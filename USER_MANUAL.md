# 📖 Apple Store Web - Hướng dẫn sử dụng

## 🎯 Dành cho người dùng cuối

### 🏠 Trang chủ
1. **Truy cập website:** `http://localhost:5000`
2. **Xem sản phẩm nổi bật:** 8 sản phẩm Apple hot nhất
3. **Navigation menu:** 
   - Trang chủ
   - Sản phẩm
   - Giỏ hàng
   - Đăng nhập/Đăng ký

### 🛍️ Mua sắm sản phẩm

#### Bước 1: Duyệt sản phẩm
- Nhấn **"Sản phẩm"** trên menu
- Xem danh sách tất cả sản phẩm Apple

#### Bước 2: Lọc sản phẩm
- **Theo danh mục:** iPhone, iPad, Mac
- **Theo khoảng giá:** Kéo thanh slider
- **Theo dung lượng:** 128GB, 256GB, 512GB, 1TB
- **Theo màu sắc:** Các màu có sẵn
- **Tìm kiếm:** Nhập tên sản phẩm

#### Bước 3: Xem chi tiết
- Nhấn vào sản phẩm muốn mua
- Xem thông tin chi tiết, hình ảnh
- Chọn dung lượng và màu sắc
- Nhấn **"Thêm vào giỏ hàng"**

#### Bước 4: Quản lý giỏ hàng
- Nhấn icon giỏ hàng (góc phải trên)
- Xem sản phẩm đã chọn
- Thay đổi số lượng hoặc xóa sản phẩm
- Nhấn **"Thanh toán"**

#### Bước 5: Đặt hàng
- Đăng nhập tài khoản (nếu chưa)
- Điền thông tin giao hàng
- Chọn phương thức thanh toán
- Nhấn **"Đặt hàng"**

### 👤 Quản lý tài khoản

#### Đăng ký tài khoản mới:
1. Nhấn **"Đăng ký"**
2. Điền thông tin:
   - Họ tên
   - Email
   - Mật khẩu (tối thiểu 6 ký tự)
   - Số điện thoại
   - Địa chỉ
3. Nhấn **"Đăng ký"**

#### Đăng nhập:
1. Nhấn **"Đăng nhập"**
2. Nhập email và mật khẩu
3. Tích **"Ghi nhớ đăng nhập"** (tùy chọn)
4. Nhấn **"Đăng nhập"**

#### Xem đơn hàng:
1. Sau khi đăng nhập, nhấn **"Đơn hàng"**
2. Xem danh sách đơn hàng đã đặt
3. Nhấn **"Chi tiết"** để xem thông tin cụ thể

### 📱 Tính năng đặc biệt

#### Tìm kiếm thông minh:
- Gõ tên sản phẩm trong ô tìm kiếm
- Hệ thống sẽ gợi ý sản phẩm phù hợp
- Nhấn vào gợi ý để xem chi tiết

#### Giỏ hàng thông minh:
- Số lượng sản phẩm hiển thị trên icon giỏ hàng
- Tự động tính tổng tiền
- Lưu trữ tạm thời trong phiên làm việc

---

## 👨‍💼 Dành cho quản trị viên

### 🔑 Đăng nhập Admin
- **Email:** `admin@applestore.com`
- **Mật khẩu:** `AppleAdmin@2025`
- Sau khi đăng nhập, truy cập `/Admin`

### 📊 Dashboard quản trị

#### Thống kê tổng quan:
- **Tổng sản phẩm:** Số lượng sản phẩm trong hệ thống
- **Tổng đơn hàng:** Số đơn hàng đã được đặt
- **Tổng khách hàng:** Số người dùng đã đăng ký
- **Tổng doanh thu:** Doanh thu từ đơn hàng đã giao

#### Thống kê theo thời gian:
- **Hôm nay:** Đơn hàng và doanh thu trong ngày
- **Tháng này:** So sánh với tháng trước
- **Đơn hàng đang xử lý:** Chờ xử lý và đang giao
- **Hoạt động:** Người dùng online, tỷ lệ chuyển đổi

### 🛍️ Quản lý sản phẩm

#### Xem danh sách sản phẩm:
- Truy cập **"Quản lý sản phẩm"**
- Xem tất cả sản phẩm với thông tin:
  - Hình ảnh
  - Tên sản phẩm
  - Thương hiệu
  - Danh mục
  - Giá
  - Trạng thái tồn kho
  - Sản phẩm nổi bật

#### Quản lý tồn kho:
- Nhấn nút **"Mắt"** để bật/tắt trạng thái còn hàng
- Sản phẩm hết hàng sẽ không hiển thị cho khách hàng

### 📦 Quản lý đơn hàng

#### Xem danh sách đơn hàng:
- Truy cập **"Quản lý đơn hàng"**
- Thông tin hiển thị:
  - Mã đơn hàng
  - Khách hàng
  - Ngày đặt
  - Tổng tiền
  - Trạng thái
  - Phương thức thanh toán

#### Cập nhật trạng thái đơn hàng:
1. Nhấn nút **"Sửa"** (dropdown)
2. Chọn trạng thái mới:
   - **Xác nhận:** Đơn hàng được xác nhận
   - **Đang giao:** Đơn hàng đang được vận chuyển
   - **Đã giao:** Đơn hàng đã giao thành công
   - **Hủy đơn:** Hủy đơn hàng

#### Xem chi tiết đơn hàng:
- Nhấn nút **"Mắt"** để xem thông tin chi tiết
- Thông tin sản phẩm, khách hàng, địa chỉ giao hàng

### 👥 Quản lý khách hàng

#### Xem danh sách khách hàng:
- Truy cập **"Quản lý khách hàng"**
- Thông tin hiển thị:
  - Tên khách hàng
  - Email
  - Số điện thoại
  - Địa chỉ
  - Vai trò (Admin/Khách hàng)
  - Trạng thái tài khoản

#### Khóa/Mở khóa tài khoản:
- Nhấn nút **"Khóa"** để khóa tài khoản khách hàng
- Nhấn nút **"Mở khóa"** để kích hoạt lại
- **Lưu ý:** Không thể khóa tài khoản admin

### 🔧 Thao tác nhanh

#### Từ Dashboard:
- **Quản lý sản phẩm Apple:** Truy cập nhanh danh sách sản phẩm
- **Quản lý đơn hàng:** Xem đơn hàng chờ xử lý
- **Quản lý khách hàng:** Xem danh sách người dùng
- **Xem Apple Store:** Quay về trang chủ website

---

## 🚨 Xử lý sự cố

### Lỗi thường gặp:

#### 1. Không đăng nhập được:
- Kiểm tra email và mật khẩu
- Đảm bảo tài khoản chưa bị khóa
- Thử đăng ký tài khoản mới

#### 2. Giỏ hàng bị mất:
- Giỏ hàng lưu trong phiên làm việc
- Không đóng trình duyệt khi mua sắm
- Đăng nhập để lưu trữ lâu dài

#### 3. Không thể đặt hàng:
- Đảm bảo đã đăng nhập
- Kiểm tra thông tin giao hàng đầy đủ
- Thử lại sau vài phút

#### 4. Admin không truy cập được:
- Kiểm tra tài khoản: `admin@applestore.com`
- Mật khẩu: `AppleAdmin@2025`
- Liên hệ kỹ thuật viên nếu vẫn lỗi

### Liên hệ hỗ trợ:
- **Email:** support@applestore.com
- **Hotline:** 1900-xxxx
- **Giờ làm việc:** 8:00 - 22:00 (T2-CN)

---
**Hướng dẫn sử dụng v1.0**  
**Cập nhật:** 20/09/2025