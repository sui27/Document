# Tóm tắt dịch vụ cơ bản

## 1. **Domain (Tên miền)**
- **Khái niệm**: Địa chỉ của một trang web trên Internet, thay thế cho địa chỉ IP.
  - Người dùng nhập tên miền vào trình duyệt để truy cập website.
  - Ví dụ: `vietnix.vn`, `google.com`, `facebook.com`.

### **Thành phần của Domain**
- **Protocol**: Giao thức (http/https).
- **Sub-domain**: Phân chia các phần khác nhau của trang web.
  - Ví dụ: `blog.vietnix.vn`, `support.vietnix.vn`.
- **Second-level Domain (SLD)**: Phần định danh chính của tên miền.
  - Ví dụ: `google` trong `google.com`.
- **Top-level Domain (TLD)**: Phần cuối cùng của tên miền.
  - Ví dụ: `.com` (thương mại), `.org` (phi lợi nhuận), `.vn` (Việt Nam).
- **Page-path**: Đường dẫn trang, đại diện cho cấu trúc thư mục trên website.
  - Ví dụ: `/webmail`.

### **Các bước để sở hữu tên miền**
1. Chọn nhà cung cấp dịch vụ.
2. Thanh toán phí đăng ký.
3. Chọn tên miền phù hợp với mục tiêu và đối tượng người dùng.

### **Tên miền quốc tế vs quốc gia**
- **Tên miền quốc tế**: Phạm vi tiếp cận rộng hơn.
- **Tên miền quốc gia**: Độ tin cậy và nội địa hóa tốt hơn.

---

## 2. **Hosting**
### **Web Hosting**
- **Khái niệm**: Không gian lưu trữ dữ liệu để triển khai website hoạt động 24/7.
  - Chia sẻ tài nguyên máy chủ như CPU, RAM.
  - Đăng ký dịch vụ là thuê một "chỗ chứa" cho dữ liệu website.

#### **Ưu điểm**
- Chi phí thấp.
- Thân thiện với người mới bắt đầu.
- Nhà cung cấp chịu trách nhiệm quản lý máy chủ.

#### **Nhược điểm**
- Không có toàn quyền kiểm soát cấu hình.
- Lượng truy cập lớn từ các website khác có thể ảnh hưởng hiệu suất.

### **SEO Hosting**
- **Khái niệm**: Hosting tối ưu cho SEO.
  - Hỗ trợ nhiều địa chỉ IP trên cùng tài khoản hosting.
  - Tránh bị Google footprint khi chạy nhiều website.

### **Email Hosting**
- **Khái niệm**: Dịch vụ lưu trữ email theo tên miền doanh nghiệp.
  - Tăng tính chuyên nghiệp và uy tín.

---

## 3. **VPS (Virtual Private Server)**
### **Khái niệm**
- Máy chủ ảo được chia từ máy chủ vật lý.
- Có quyền truy cập và quản lý tương tự máy chủ chuyên dụng.

### **Cách hoạt động**
- Nhà cung cấp cài đặt phần mềm giám sát máy ảo trên máy chủ vật lý.
- Chia sẻ tài nguyên như RAM, CPU, disk.

### **Ứng dụng của VPS**
- Phát triển dự án.
- Lưu trữ website đa dịch vụ.
- Nơi lưu trữ tài liệu, hình ảnh, video.
- Hệ thống email doanh nghiệp.
- Máy chủ game.

### **Dedicated Server**
- **Khái niệm**: Máy chủ vật lý chuyên dụng tại datacenter.
- **Đặc điểm**:
  - Tài nguyên lớn, không chia sẻ với hệ thống khác.
  - Phù hợp cho doanh nghiệp lớn, tài chính mạnh.
  - Cấu hình linh hoạt, đáp ứng nhu cầu mở rộng phần cứng.

---

## 4. **Colocation**
- **Khái niệm**: Dịch vụ cung cấp không gian và tài nguyên mạng tại datacenter.
  - Doanh nghiệp sở hữu máy chủ riêng, đặt tại môi trường chuyên nghiệp.
  - Datacenter đảm bảo môi trường an toàn và liên tục.

---

## 5. **Kiến thức phần cứng**
### **CPU**
- **Core**: Xử lý nhiều tác vụ đồng thời.
- **Thread**: Luồng CPU, thực hiện bao nhiêu tác vụ cùng lúc.
  - Ví dụ: CPU 4 core, 8 thread => Xử lý 8 tác vụ đồng thời.
- **Xung nhịp**: Tốc độ xử lý, đo bằng GHz hoặc MHz.
  - Không chỉ xung nhịp, số Core, Luồng và Cache cũng ảnh hưởng hiệu suất.

### **RAM**
- **Khái niệm**: Bộ nhớ tạm thời, tốc độ cao.
- **Đặc điểm**:
  - Tốc độ đo bằng Bus RAM (MHz) và CAS latency.
  - Bus RAM phổ biến: 1600MHz, 2400MHz, 3200MHz.

### **Disk (Ổ đĩa)**
- **HDD**: Dữ liệu lưu trữ trong đĩa từ, tốc độ thấp (80MB-160MB/s).
- **SSD**: Tốc độ cao hơn HDD, bền hơn, không có bộ phận cơ học.
- **NVMe**: Nhanh hơn SSD SATA 7-10 lần, độ trễ thấp.

### **RAID**
- **Khái niệm**: Công nghệ lưu trữ trên nhiều ổ đĩa.
  - **RAID 0**: Tăng tốc độ, không dự phòng dữ liệu.
  - **RAID 1**: Dự phòng dữ liệu, dung lượng giảm.
  - **RAID 10**: Kết hợp RAID 0 và RAID 1.

---

## 6. **Mạng và bảo mật tại Datacenter**
### **Kết nối**
- Băng thông lớn, độ trễ thấp, kết nối giữa các hệ thống.

### **Bảo mật và Dự phòng**
- Dữ liệu được bảo vệ với hệ thống bảo mật vật lý và phần mềm.
- Hệ thống dự phòng đảm bảo dịch vụ luôn sẵn sàng.

### **Quản lý và Giám sát**
- Giám sát hoạt động liên tục để đảm bảo ổn định.
- Xử lý sự cố nhanh chóng, tự động hóa giám sát.
