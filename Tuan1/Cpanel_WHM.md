# Tổng quan về cPanel và WHM

## cPanel

### Giao diện cPanel
Khi đăng nhập vào giao diện cPanel, người dùng cần nắm rõ bốn khu vực chính như sau:

1. **Thanh tìm kiếm (Search Bar)**: Cho phép người dùng nhanh chóng tìm kiếm các tính năng bằng cách nhập từ khóa (ví dụ: "File Manager").
2. **Thông tin chung (General Information)**: Hiển thị các thông tin cơ bản về gói hosting và server.
3. **Thống kê (Statistics)**: Bao gồm các số liệu như RAM, CPU, số tiến trình, Addon Domain, tài khoản email, và băng thông đang sử dụng.
4. **Tính năng (Features)**: Hiển thị tất cả các chức năng mà quản trị viên cho phép người dùng sử dụng.

### Các tính năng chính

#### Quản lý Email
- **Tài khoản Email (Email Accounts)**: Tạo, xóa và quản lý tài khoản email.
- **Chuyển tiếp Email (Forwarders)**: Chuyển tiếp email đến địa chỉ email khác.
- **Định tuyến Email (Email Routing)**: Luôn thiết lập là Local Mail Exchanger.
- **Trả lời tự động (Autoresponders)**: Cấu hình email trả lời tự động.
- **Địa chỉ mặc định (Default Address)**: Cấu hình Catch-all Email để nhận email gửi tới các địa chỉ không tồn tại.
- **Danh sách gửi thư (Mailing Lists)**: Tạo nhóm email để gửi thông báo đồng thời tới nhiều người.
- **Theo dõi trạng thái email (Track Delivery)**: Theo dõi trạng thái của email đã gửi.
- **Bộ lọc thư rác (Spam Filters)**: Quản lý thư rác bằng Apache SpamAssassin™.
- **Dung lượng email (Email Disk Usage)**: Kiểm tra dung lượng lưu trữ của email.
- **ASSP Antispam**: Cấu hình bảo vệ chống spam nâng cao.
- **Global Email filter**: áp dụng rule filter cho toàn bộ email.
- **Email Filter**: Áp dụng cho 1 email được cấu hình

#### Quản lý Tệp tin
- **Trình quản lý tệp (File Manager)**: Tải lên, xóa, chỉnh sửa, nén và giải nén tệp. Hỗ trợ hiển thị các tệp ẩn như .htaccess.
- **Hình ảnh (Images)**: Công cụ chỉnh sửa hình ảnh cơ bản.
- **Bảo mật thư mục (Directory Privacy)**: Cài đặt bảo mật bằng user/password cho thư mục.
- **Dung lượng đĩa (Disk Usage)**: Kiểm tra mức sử dụng dung lượng đĩa.
- **Đĩa web (Web Disk)**: Quản lý dữ liệu web tương tự Google Drive hoặc OneDrive.
- **Tài khoản FTP (FTP Accounts)**: Tạo tài khoản FTP và phân quyền truy cập thư mục.
- **Sao lưu (Backup)**: Bao gồm Wizard và JetBackup 5 để phục hồi toàn bộ hoặc chọn lọc dữ liệu.

#### Quản lý Cơ sở Dữ liệu
- **phpMyAdmin**: Quản lý cơ sở dữ liệu MySQL.
- **Cơ sở dữ liệu MySQL (MySQL Databases)**: Tạo cơ sở dữ liệu, tài khoản người dùng và phân quyền.
- **Wizard MySQL**: Hướng dẫn từng bước để tạo và cấu hình cơ sở dữ liệu.
- **Remote MySQL**: Kích hoạt truy cập từ xa cho cơ sở dữ liệu.

#### Quản lý Tên Miền và DNS
- **Tên miền (Domains)**: Thêm, xóa hoặc chuyển hướng tên miền.
- **Trình chỉnh sửa vùng (Zone Editor)**: Quản lý các bản ghi DNS.
- **DNS động (Dynamic DNS)**: Cập nhật DNS cho các tên miền phụ.

#### Thống kê và Nhật ký
- **Khách truy cập (Visitors)**: Xem nhật ký truy cập.
- **Lỗi (Errors)**: Nhật ký lỗi Apache.
- **Băng thông (Bandwidth)**: Thống kê lưu lượng truy cập theo từng ngày.
- **Nhật ký thô (Raw Access)**: Tải xuống nhật ký thô để phân tích.

#### Bảo mật
- **Truy cập SSH (SSH Access)**: Kích hoạt truy cập bằng SSH key.
- **Chặn IP (IP Blocker)**: Ngăn chặn IP không mong muốn truy cập website.
- **Quản lý SSL/TLS**: Cấu hình và quản lý chứng chỉ SSL.
- **Xác thực hai lớp (Two-Factor Authentication)**: Tăng cường bảo mật khi đăng nhập.
- **Imunify360**: Quét và bảo vệ khỏi virus tự động.

#### Công cụ Nâng cao
- **Quản lý Ứng dụng**: Cài đặt các ứng dụng như Node.js và quản lý phiên bản PHP.
- **Công việc định kỳ (Cron Jobs)**: Lên lịch tự động hóa các tác vụ.
- **Truy cập Terminal**: Dành cho người dùng nâng cao chạy lệnh trực tiếp.
- **Trang lỗi (Error Pages)**: Tùy chỉnh giao diện các trang lỗi của Apache.

---

## WHM (Web Host Manager)

### Quản lý Tài khoản và Tên miền
- **Đổi Tên miền Chính (Modify Primary Domain)**: Thay đổi tên miền chính của tài khoản thông qua mục "Modify an Account". Đảm bảo không có xung đột với các tên miền đã tồn tại.
- **Di chuyển và Chuyển tài khoản (Migrate and Transfer Accounts)**: Sử dụng công cụ Transfer Tool với xác thực SSH Public Key để di chuyển tài khoản giữa các server.

### Các Lệnh Terminal
- **Tải lại Hosting (Reload Hosting)**: Dùng lệnh `cagefs -m <user>`.
- **Vị trí Nhật ký (Log Locations)**:
  - Tên miền không có SSL: `/var/log/apache2/domlogs/<domain>`.
  - Tên miền có SSL: `/var/log/apache2/domlogs/<domain>-ssl_log`.
- **Kiểm tra Tiến trình (Process Monitoring)**: Xem các tiến trình đang chạy bằng lệnh `ps aux | grep <user>`.

### Quản lý Tên miền Phụ
- Xác định tài khoản nào đang sử dụng tên miền phụ thông qua terminal hoặc giao diện GUI. Lệnh:
  - `cat /etc/userdatadomains | grep <domain>`

### PHP X-Ray
PHP X-Ray giúp theo dõi thời gian thực thi các chức năng PHP để chẩn đoán hiệu suất website. Thao tác qua plugin CloudLinux Manager:
- Thiết lập URL cần theo dõi.
- Cấu hình thời gian hoặc số lần yêu cầu.
- Phân tích các chức năng gây chậm và tối ưu hóa nếu cần.

---
