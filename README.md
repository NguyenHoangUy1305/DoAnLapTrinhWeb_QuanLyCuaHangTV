# 📺 N&U STORE – HỆ THỐNG WEBSITE THƯƠNG MẠI ĐIỆN TỬ, MUA BÁN TRẢ GÓP & BẢO HÀNH TIVI (PHP & MYSQL)

<p align="center">
  <img src="https://img.shields.io/badge/PHP-7.4_%2F_8.x-777BB4?style=for-the-badge&logo=php&logoColor=white" alt="PHP" />
  <img src="https://img.shields.io/badge/Database-MySQL_InnoDB-4479A1?style=for-the-badge&logo=mysql&logoColor=white" alt="MySQL" />
  <img src="https://img.shields.io/badge/Frontend-HTML5_--_CSS3_--_JS-E34F26?style=for-the-badge&logo=html5&logoColor=white" alt="Frontend" />
  <img src="https://img.shields.io/badge/Security-BCRYPT_Hash-success?style=for-the-badge" alt="BCRYPT" />
  <img src="https://img.shields.io/badge/Feature-Tr%E1%BA%A3_G%C3%B3p_%26_B%E1%BA%A3o_H%C3%A0nh-orange?style=for-the-badge" alt="Trả Góp & Bảo Hành" />
</p>

---

## 📌 1. TỔNG QUAN ĐỀ TÀI
* **Môn học:** Lập trình Web
* **Đơn vị đào tạo:** Khoa Công nghệ Thông tin – Trường Đại học An Giang (ĐHQG TP.HCM)
* **Sinh viên thực hiện:**
  - **Nguyễn Hoàng Uy** (MSSV: `DTH235812`) – Lớp: DH24TH3
  - **Thái Vĩnh Nghi** (MSSV: `DTH235704`) – Lớp: DH24TH3

**N&U STORE** là nền tảng thương mại điện tử chuyên ngành thiết bị hiển thị và giải trí thông minh (Smart TV 4K, 8K, OLED, QLED, Mini LED, Soundbar,...). Hệ thống kết hợp giữa **Cổng mua sắm B2C trực tuyến cho khách hàng** và **Hệ thống điều hành doanh nghiệp (ERP/POS) cho ban quản trị**.

Đặc biệt, hệ thống giải quyết bài toán tài chính phức tạp thông qua **Phân hệ Mua hàng trả góp (Installment Loan)** và **Quy trình Bảo hành điện tử & Đổi trả hàng lỗi**.

---

## 💡 2. CÁC TÍNH NĂNG ĐỘC ĐÁO & NGHIỆP VỤ NỔI BẬT

1. **Phân hệ Mua hàng Trả góp (Installment Credit Management):**
   - Cho phép khách hàng chọn gói mua trả góp theo tỷ lệ trả trước (0%, 20%, 30%, 50%) và kỳ hạn linh hoạt (3, 6, 9, 12 tháng).
   - Ban quản trị xét duyệt hồ sơ trực tuyến, tự động tính toán số tiền góp định kỳ hàng tháng và lãi suất.
   - Bảng `tragop_thanhtoan` theo dõi lịch sử nộp tiền từng đợt, nhắc nợ và tính toán dư nợ còn lại.
2. **Hệ thống Bảo hành Điện tử & Đổi trả sản phẩm:**
   - Quản lý serial máy và kích hoạt thời hạn bảo hành điện tử khi đơn hàng thành công.
   - Tiếp nhận yêu cầu đổi trả hàng trực tuyến (`doitra_yeucau.php`), ban quản trị xử lý và phân loại lỗi.
   - Tự động xuất phiếu bảo hành (`filexuatphieubachanh`) và xuất hóa đơn chi tiết (`filexuathoadonchitiet`).
3. **Bảo mật & Phân quyền Đa tầng:**
   - Mật khẩu tài khoản khách hàng và nhân viên được mã hóa băm an toàn bằng thuật toán **BCRYPT** (`MatKhauHash`).
   - Phân quyền rõ ràng 3 nhóm: **Khách hàng**, **Nhân viên bán hàng (QuyenHan=0)** và **Quản trị viên Admin (QuyenHan=1)**.
   - Tính năng quên mật khẩu, đổi mật khẩu và hệ thống **Audit Log (`nhatky_hethong`)** lưu vết mọi thao tác.

---

## 🗄️ 3. THIẾT KẾ CƠ SỞ DỮ LIỆU (13 BẢNG CHUẨN HÓA INNODB)

Cơ sở dữ liệu: `quanlycuahangtivi` được thiết kế theo chuẩn 3NF, cấu hình `utf8mb4_general_ci`:

* **Nhóm Quản lý Khách hàng & Nhân sự:**
  - `khachhang`: Thông tin khách hàng, số điện thoại, địa chỉ nhận hàng, mật khẩu BCRYPT.
  - `nhanvien`: Cán bộ nhân viên, chức vụ, quyền hạn (Admin / Bán hàng).
  - `nhatky_hethong`: Audit log ghi nhận thao tác người dùng, thời gian và sự kiện.
* **Nhóm Danh mục Sản phẩm:**
  - `sanpham`: Danh sách TV, giá niêm yết, phần trăm giảm giá, số lượng tồn kho, hình ảnh, thông số kỹ thuật.
  - `loaisanpham`: Phân loại công nghệ (Smart TV 4K, Android TV, OLED, QLED, Mini LED, 8K, The Frame,...).
  - `hangsanxuat`: Danh mục thương hiệu (Sony, Samsung, LG, TCL, Casper, Xiaomi, Sharp,...).
* **Nhóm Giao dịch & Kho hàng:**
  - `hoadon` & `hoadon_chitiet`: Giao dịch mua hàng, tổng tiền, phương thức thanh toán (Tiền mặt / Chuyển khoản QR).
  - `nhacungcap`: Danh mục đơn vị cung ứng hàng hóa.
  - `phieunhap` & `phieunhap_chitiet`: Quản lý nhập hàng từ nhà sản xuất, cập nhật giá vốn và tồn kho.
* **Nhóm Trả góp & Dịch vụ Hậu mãi:**
  - `tragop`: Hồ sơ đăng ký mua trả góp, kỳ hạn, lãi suất, trạng thái duyệt.
  - `tragop_chitiet`: Sản phẩm trong hợp đồng trả góp.
  - `tragop_thanhtoan`: Lịch sử đóng tiền từng tháng, biên nhận thanh toán.
  - `baohanh`: Quản lý thời hạn bảo hành và thông tin kích hoạt máy.

---

## 📂 4. CẤU TRÚC THƯ MỤC SOURCE CODE

```text
DoAnLapTrinhWeb_QuanLyCuaHangTV/
├── MoTa_CoSoDuLieu.txt         # Tài liệu đặc tả kỹ thuật CSDL chi tiết (700+ dòng)
├── quanlycuahangtivi.sql       # Script import CSDL MySQL hoàn chỉnh
├── trang_chu.php               # Trang chủ hiển thị banner, sản phẩm nổi bật
├── san_pham.php                # Danh mục sản phẩm (Lọc theo hãng & công nghệ TV)
├── chi_tiet_san_pham.php       # Trang chi tiết thông số kỹ thuật, đánh giá review
├── gio_hang.php                # Giỏ hàng mua sắm trực tuyến
├── thanh_toan.php              # Thanh toán đơn hàng (Hỗ trợ quét mã QR Chuyển khoản)
├── dang_ky.php & login.php     # Đăng ký / Đăng nhập tài khoản BCRYPT
├── doitra_yeucau.php           # Cổng tiếp nhận yêu cầu đổi trả hàng bảo hành
├── filexuathoadonchitiet/      # Module kết xuất hóa đơn bán hàng chi tiết
├── filexuatphieubachanh/       # Module kết xuất phiếu bảo hành điện tử
├── thu_vien/                   # Hàm kết nối CSDL và thư viện dùng chung
│   └── connect.php
├── uploads/                    # Thư mục lưu trữ hình ảnh sản phẩm & chứng từ
├── admin/                      # Cổng Quản trị viên & Nhân viên (Admin Portal)
│   ├── index.php               # Dashboard thống kê doanh thu và đơn hàng
│   ├── san_pham_them.php       # Thêm / Sửa / Xóa sản phẩm
│   ├── hoa_don_danh_sach.php   # Quản lý hóa đơn bán hàng
│   ├── tra_gop_duyet.php       # Phê duyệt hồ sơ mua hàng trả góp
│   └── doi_tra_xuly.php        # Tiếp nhận & xử lý yêu cầu bảo hành đổi trả
└── README.md
```

---

## 🚀 5. HƯỚNG DẪN CÀI ĐẶT & CHẠY LOCAL (XAMPP)

### Yêu cầu:
* Đã cài đặt **XAMPP** (hỗ trợ PHP 7.4 hoặc PHP 8.x + MySQL/MariaDB).

### Các bước cài đặt:
1. **Clone mã nguồn vào thư mục `htdocs` của XAMPP:**
   ```bash
   cd C:\xampp\htdocs
   git clone https://github.com/NguyenHoangUy1305/DoAnLapTrinhWeb_QuanLyCuaHangTV.git
   ```
2. **Khởi động dịch vụ:**
   - Mở **XAMPP Control Panel**, bấm **Start** cho cả **Apache** và **MySQL**.
3. **Import Cơ sở dữ liệu:**
   - Mở trình duyệt, truy cập `http://localhost/phpmyadmin`.
   - Tạo Database mới với tên: `quanlycuahangtivi`, cấu hình Collation `utf8mb4_general_ci`.
   - Chọn tab **Import**, chọn file `quanlycuahangtivi.sql` trong thư mục dự án và bấm **Import**.
4. **Kiểm tra cấu hình kết nối:**
   - Mở file `thu_vien/connect.php`, đảm bảo thông tin kết nối đúng máy bạn:
     ```php
     $conn = mysqli_connect("localhost", "root", "", "quanlycuahangtivi");
     ```
5. **Truy cập ứng dụng:**
   - Trang người dùng: `http://localhost/DoAnLapTrinhWeb_QuanLyCuaHangTV/trang_chu.php`
   - Trang quản trị Admin: `http://localhost/DoAnLapTrinhWeb_QuanLyCuaHangTV/admin/`

---

## 👨‍💻 6. NHÓM TÁC GIẢ
* **Nguyễn Hoàng Uy** – *Full-stack Web PHP, Hệ thống Trả góp & CSDL* – [`NguyenHoangUy1305`](https://github.com/NguyenHoangUy1305)
* **Thái Vĩnh Nghi** – *Giao diện Frontend, Hệ thống Đổi trả & Quản trị* – [`ThaiVinhNghi1207`](https://github.com/ThaiVinhNghi1207)

*Khoa Công nghệ Thông tin – Trường Đại học An Giang (ĐHQG TP.HCM)*
