# 🔧 Apple Store Web - Hướng dẫn kỹ thuật

## 📋 Mục lục
1. [Kiến trúc hệ thống](#kiến-trúc-hệ-thống)
2. [Models và Database](#models-và-database)
3. [Controllers chi tiết](#controllers-chi-tiết)
4. [Views và UI](#views-và-ui)
5. [Authentication & Authorization](#authentication--authorization)
6. [Session Management](#session-management)
7. [API Documentation](#api-documentation)
8. [Performance & Optimization](#performance--optimization)

## 🏗️ Kiến trúc hệ thống

### Pattern sử dụng:
- **MVC Pattern** - Model-View-Controller
- **Repository Pattern** - Qua Entity Framework
- **Dependency Injection** - Built-in ASP.NET Core DI
- **Session State** - Cho giỏ hàng

### Luồng xử lý request:
```
Request → Middleware → Controller → Service/Repository → Database
                                 ↓
Response ← View ← ViewModel ← Controller
```

## 🗃️ Models và Database

### 1. ApplicationUser
```csharp
public class ApplicationUser : IdentityUser
{
    public string Name { get; set; }
    public string? Phone { get; set; }
    public string? Address { get; set; }
    public string Role { get; set; } = "customer";
    public ICollection<Order> Orders { get; set; }
}
```

### 2. Product
```csharp
public class Product
{
    public string Id { get; set; }
    public string Name { get; set; }
    public string Brand { get; set; }
    public decimal Price { get; set; }
    public decimal? OriginalPrice { get; set; }
    public string Description { get; set; }
    public string Images { get; set; } // JSON array
    public string StorageOptions { get; set; } // JSON array
    public string Colors { get; set; } // JSON array
    public string Category { get; set; }
    public string ProductType { get; set; }
    public string Processor { get; set; }
    public string DisplaySize { get; set; }
    public string KeyFeatures { get; set; } // JSON array
    public bool Featured { get; set; }
    public bool InStock { get; set; }
    public double Rating { get; set; }
    public int Reviews { get; set; }
    public DateTime CreatedAt { get; set; }
}
```

### 3. Order & OrderItem
```csharp
public class Order
{
    public string Id { get; set; }
    public string UserId { get; set; }
    public string UserName { get; set; }
    public decimal Total { get; set; }
    public string Status { get; set; } // pending, confirmed, shipping, delivered, cancelled
    public DateTime CreatedAt { get; set; }
    public string ShippingAddress { get; set; }
    public string PaymentMethod { get; set; }
    public ApplicationUser User { get; set; }
    public ICollection<OrderItem> Items { get; set; }
}

public class OrderItem
{
    public int Id { get; set; }
    public string OrderId { get; set; }
    public string ProductId { get; set; }
    public int Quantity { get; set; }
    public string StorageOption { get; set; }
    public string Color { get; set; }
    public decimal UnitPrice { get; set; }
    public Order Order { get; set; }
    public Product Product { get; set; }
}
```

### 4. CartItem (Session-based)
```csharp
public class CartItem
{
    public string ProductId { get; set; }
    public string ProductName { get; set; }
    public string ProductBrand { get; set; }
    public decimal Price { get; set; }
    public string Image { get; set; }
    public int Quantity { get; set; }
    public string StorageOption { get; set; }
    public string Color { get; set; }
}
```

## 🎮 Controllers chi tiết

### 1. HomeController
```csharp
public async Task<IActionResult> Index()
{
    // Lấy 8 sản phẩm nổi bật đang có sẵn
    var featuredProducts = await _context.Products
        .Where(p => p.Featured && p.InStock)
        .Take(8)
        .ToListAsync();
    return View(featuredProducts);
}
```

### 2. ProductsController
**Tính năng chính:**
- Lọc sản phẩm theo nhiều tiêu chí
- Tìm kiếm AJAX
- Phân trang (có thể thêm)

```csharp
public async Task<IActionResult> Index(FilterState filter)
{
    var query = _context.Products.AsQueryable();
    
    // Apply filters
    if (!string.IsNullOrEmpty(filter.Category))
        query = query.Where(p => p.Category == filter.Category);
    
    if (!string.IsNullOrEmpty(filter.Search))
        query = query.Where(p => p.Name.Contains(filter.Search));
    
    // ... more filters
    
    var products = await query.Where(p => p.InStock).ToListAsync();
    return View(products);
}
```

### 3. CartController
**Session-based cart management:**
```csharp
private List<CartItem> GetCart()
{
    var cartJson = HttpContext.Session.GetString(CartSessionKey);
    return string.IsNullOrEmpty(cartJson) 
        ? new List<CartItem>() 
        : JsonSerializer.Deserialize<List<CartItem>>(cartJson);
}

private void SaveCart(List<CartItem> cart)
{
    var cartJson = JsonSerializer.Serialize(cart);
    HttpContext.Session.SetString(CartSessionKey, cartJson);
}
```

### 4. AdminController
**Authorization check:**
```csharp
public async Task<IActionResult> Index()
{
    var user = await _userManager.GetUserAsync(User);
    if (user?.Role != "admin")
        return RedirectToAction("AccessDenied", "Account");
    
    // Admin dashboard logic
}
```

## 🎨 Views và UI

### Layout Structure
```
_Layout.cshtml
├── Header (Navigation)
├── Main Content (@RenderBody())
└── Footer
```

### Bootstrap Components sử dụng:
- **Cards** - Product display
- **Modals** - Confirmations
- **Forms** - User input
- **Badges** - Status indicators
- **Buttons** - Actions
- **Tables** - Data display

### JavaScript Libraries:
- **jQuery** - DOM manipulation
- **Bootstrap JS** - UI components
- **Font Awesome** - Icons

## 🔐 Authentication & Authorization

### ASP.NET Identity Configuration:
```csharp
builder.Services.AddIdentity<ApplicationUser, IdentityRole>(options =>
{
    options.Password.RequireDigit = true;
    options.Password.RequireLowercase = true;
    options.Password.RequireNonAlphanumeric = false;
    options.Password.RequireUppercase = false;
    options.Password.RequiredLength = 6;
    options.User.RequireUniqueEmail = true;
    options.SignIn.RequireConfirmedEmail = false;
})
```

### Role-based Authorization:
- **Admin:** Truy cập `/Admin/*`
- **Customer:** Truy cập `/Orders/*`
- **Anonymous:** Truy cập public pages

### Custom Authorization Check:
```csharp
var user = await _userManager.GetUserAsync(User);
if (user?.Role != "admin")
    return RedirectToAction("AccessDenied", "Account");
```

## 🗂️ Session Management

### Session Configuration:
```csharp
builder.Services.AddSession(options =>
{
    options.IdleTimeout = TimeSpan.FromMinutes(30);
    options.Cookie.HttpOnly = true;
    options.Cookie.IsEssential = true;
});
```

### Session Usage:
- **Shopping Cart** - Lưu trữ tạm thời
- **User Preferences** - Filters, sorting
- **Temporary Data** - Flash messages

## 📡 API Documentation

### Cart APIs

#### POST /Cart/AddToCart
```json
{
    "productId": "iphone-15-pro",
    "storageOption": "256GB",
    "color": "Natural Titanium",
    "quantity": 1
}
```

#### GET /Cart/GetCartCount
```json
{
    "count": 3
}
```

### Admin APIs

#### POST /Admin/UpdateOrderStatus
```json
{
    "orderId": "ORD001",
    "status": "confirmed"
}
```

#### POST /Admin/ToggleProductStock
```json
{
    "productId": "iphone-15-pro"
}
```

### Search API

#### GET /Products/Search?term=iphone
```json
[
    {
        "id": "iphone-15-pro",
        "name": "iPhone 15 Pro",
        "brand": "Apple",
        "price": 28990000,
        "image": "https://..."
    }
]
```

## ⚡ Performance & Optimization

### Database Optimization:
- **Indexes** trên các trường thường query
- **Eager Loading** cho related data
- **Async/Await** cho tất cả database operations

### Caching Strategy:
- **Session State** cho cart
- **ViewBag/ViewData** cho temporary data
- **Static files** caching

### Query Optimization:
```csharp
// Good - Specific fields only
var products = await _context.Products
    .Where(p => p.Featured && p.InStock)
    .Select(p => new { p.Id, p.Name, p.Price })
    .ToListAsync();

// Avoid - Loading full entities unnecessarily
var products = await _context.Products
    .Include(p => p.OrderItems)
    .ToListAsync();
```

### Frontend Optimization:
- **Minified CSS/JS**
- **CDN** cho Bootstrap, jQuery
- **Lazy loading** cho images
- **AJAX** cho dynamic content

## 🔍 Debugging & Logging

### Logging Configuration:
```csharp
builder.Logging.AddConsole();
builder.Logging.AddDebug();
```

### Common Debug Points:
1. **Authentication** - User roles
2. **Database** - Query execution
3. **Session** - Cart state
4. **API calls** - Request/Response

### Debug Controller:
```csharp
public async Task<IActionResult> CheckAdmin()
{
    var admin = await _userManager.FindByEmailAsync("admin@applestore.com");
    return Json(new { 
        AdminExists = admin != null,
        AdminRole = admin?.Role 
    });
}
```

## 🚀 Deployment Considerations

### Production Settings:
- **Connection Strings** - Use production database
- **HTTPS** - Force SSL
- **Error Handling** - Custom error pages
- **Logging** - File-based logging

### Security Checklist:
- ✅ HTTPS enabled
- ✅ CSRF protection
- ✅ SQL Injection protection (EF Core)
- ✅ XSS protection (Razor encoding)
- ✅ Authentication required for sensitive operations

---
**Tài liệu kỹ thuật v1.0**  
**Cập nhật:** 20/09/2025