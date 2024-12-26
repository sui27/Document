# Mô hình Reverse Proxy với Nginx và Apache

Mô hình reverse proxy kết hợp giữa **Nginx** và **Apache** là một cách phổ biến để triển khai các ứng dụng web, đặc biệt khi cần kết hợp nhiều công nghệ khác nhau như WordPress (chạy trên Apache) và Laravel (chạy trên Apache). Trong mô hình này, **Nginx** hoạt động như một **reverse proxy** để chuyển tiếp các yêu cầu HTTP/HTTPS tới **Apache**, nơi các ứng dụng web thực sự chạy.

## **Giải thích về mô hình trên:**

### 1. **Reverse Proxy với Nginx:**
- **Nginx** hoạt động như một reverse proxy, nhận các yêu cầu từ người dùng và chuyển tiếp chúng tới các ứng dụng chạy trên Apache.
- **Nguyên lý hoạt động**: Khi người dùng gửi yêu cầu đến các domain như `wpadmin.nguyenbinh.site` hoặc `laravel.nguyenbinh.site`, **Nginx** sẽ nhận yêu cầu và chuyển tiếp tới các port của Apache (8080 hoặc 8443) nơi các ứng dụng WordPress và Laravel đang chạy.
- **SSL/TLS Termination**: Nginx cũng chịu trách nhiệm xử lý kết nối SSL/TLS (với chứng chỉ Let's Encrypt), giảm tải cho Apache.
- **Lý do dùng Nginx làm reverse proxy**:
    - **Hiệu suất cao**: Nginx có thể xử lý một lượng lớn yêu cầu đồng thời với tài nguyên hệ thống ít hơn so với Apache.
    - **Xử lý tĩnh tốt hơn**: Nginx được tối ưu hóa để phục vụ các tệp tĩnh (như hình ảnh, CSS, JavaScript) nhanh chóng và hiệu quả.

### 2. **Apache Web Server:**
- **Apache** được cấu hình để phục vụ các ứng dụng web động như **WordPress** và **Laravel**, vì Apache hỗ trợ rất tốt PHP thông qua mô-đun như `mod_php`.
- **Lý do dùng Apache**:
    - **Tương thích tốt với WordPress**: WordPress yêu cầu các tính năng đặc biệt của Apache như `.htaccess` và các mô-đun Apache.
    - **Xử lý PHP tốt**: Apache có thể dễ dàng xử lý các yêu cầu PHP nhờ vào `mod_php` hoặc FastCGI.
- **Cấu hình SSL trên Apache**: Apache xử lý kết nối HTTPS cho các ứng dụng chạy trên port 8443, khi người dùng truy cập bằng HTTPS.

### 3. **MySQL**:
- **MySQL** được cài đặt để lưu trữ dữ liệu cho cả **WordPress** và **Laravel**.
- Hai cơ sở dữ liệu được tạo là `wordpress_db` và `laravel_db`, mỗi cơ sở dữ liệu sẽ có người dùng riêng (`wp_user`, `laravel_user`) và các quyền truy cập thích hợp.

### 4. **Tạo Virtual Hosts và Cấu hình Apache/Nginx**:
- **Apache Virtual Hosts**: Được cấu hình cho từng domain (`wpadmin.nguyenbinh.site` và `laravel.nguyenbinh.site`), với các cấu hình riêng biệt cho port 8080 (HTTP) và 8443 (HTTPS).
- **Nginx Server Blocks**: Cấu hình cho các domain trên Nginx để proxy yêu cầu đến Apache.

## **Lý do sử dụng Nginx và Apache**:

### **Ưu điểm của Nginx:**
1. **Hiệu suất cao**:
    - Nginx xử lý các kết nối đồng thời rất tốt nhờ vào mô hình bất đồng bộ (asynchronous) và ít sử dụng tài nguyên hơn so với Apache.
    - Điều này giúp giảm tải cho hệ thống, đặc biệt khi có nhiều yêu cầu HTTP đồng thời.

2. **Xử lý các yêu cầu tĩnh tốt hơn**:
    - Nginx rất nhanh trong việc phục vụ các tệp tĩnh (như hình ảnh, CSS, JavaScript) và có thể tối ưu hóa băng thông và thời gian tải trang.

3. **SSL/TLS Termination**:
    - Nginx có thể đảm nhận việc giải mã SSL, giảm tải cho Apache và giúp tăng hiệu suất tổng thể.

4. **Cấu hình đơn giản**:
    - Cấu hình của Nginx rất dễ hiểu và dễ bảo trì, đặc biệt khi làm reverse proxy hoặc load balancing.

### **Nhược điểm của Nginx**:
1. **Khó cấu hình cho ứng dụng động (như PHP)**:
    - Mặc dù Nginx rất mạnh mẽ, nhưng nó không thể xử lý PHP trực tiếp như Apache. Vì vậy, cần phải cấu hình thêm FastCGI hoặc sử dụng Apache làm backend.
   
2. **Hỗ trợ hạn chế đối với .htaccess**:
    - Nginx không hỗ trợ file `.htaccess` như Apache, điều này có thể là một hạn chế trong một số trường hợp (chẳng hạn như đối với các ứng dụng WordPress).

### **Ưu điểm của Apache:**
1. **Hỗ trợ tốt với PHP**:
    - Apache được tích hợp chặt chẽ với PHP thông qua `mod_php`, điều này giúp Apache dễ dàng xử lý các ứng dụng PHP như WordPress và Laravel.
   
2. **Tính linh hoạt với .htaccess**:
    - Apache hỗ trợ `.htaccess`, giúp quản trị viên dễ dàng cấu hình các thiết lập cho ứng dụng mà không cần phải thay đổi cấu hình toàn cục của máy chủ.

3. **Hỗ trợ module phong phú**:
    - Apache có một lượng lớn các mô-đun để mở rộng chức năng, chẳng hạn như `mod_rewrite` cho các URL đẹp trong WordPress.

### **Nhược điểm của Apache**:
1. **Hiệu suất kém hơn so với Nginx**:
    - Apache sử dụng mô hình đa tiến trình (multi-threaded), điều này dẫn đến việc sử dụng tài nguyên hệ thống nhiều hơn khi xử lý một lượng lớn yêu cầu đồng thời.

2. **Khó mở rộng**:
    - Apache không có khả năng mở rộng tốt như Nginx khi xử lý lượng truy cập lớn.

## **Kết luận**:
- **Nginx** được sử dụng làm reverse proxy để tận dụng khả năng xử lý tốc độ cao, ít tốn tài nguyên và khả năng xử lý SSL.
- **Apache** được sử dụng để chạy các ứng dụng PHP động như **WordPress** và **Laravel**, vì nó hỗ trợ PHP tốt hơn và có khả năng sử dụng `.htaccess` cho các cấu hình ứng dụng dễ dàng.
- Mô hình này kết hợp ưu điểm của cả hai phần mềm: Nginx làm việc tốt với các yêu cầu tĩnh và SSL, còn Apache chuyên xử lý các ứng dụng PHP động.
