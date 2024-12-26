# Giới thiệu về Reverse Proxy và mô hình Reverse Proxy với Nginx và Apache

## Giới thiệu về Reverse Proxy

**Reverse Proxy** là một loại proxy server, nhưng thay vì đứng giữa người dùng và internet (như forward proxy), Reverse Proxy đứng giữa người dùng và các máy chủ backend (các máy chủ thực hiện xử lý yêu cầu ứng dụng). Khi người dùng gửi yêu cầu HTTP/HTTPS, yêu cầu không trực tiếp được chuyển đến máy chủ thực sự, mà sẽ được chuyển đến Reverse Proxy. Reverse Proxy sẽ tiếp nhận yêu cầu và sau đó chuyển tiếp yêu cầu đó tới các máy chủ backend phù hợp (ví dụ: Apache). Khi máy chủ backend xử lý yêu cầu và trả về kết quả, Reverse Proxy sẽ tiếp tục chuyển kết quả đó đến người dùng cuối.

**Reverse Proxy** có nhiều ứng dụng trong việc cải thiện bảo mật, hiệu suất và khả năng mở rộng của các ứng dụng web. Một trong những ứng dụng phổ biến của Reverse Proxy là kết hợp với các web server như Nginx và Apache để tối ưu hóa việc xử lý yêu cầu HTTP/HTTPS.

## Giải thích về mô hình Reverse Proxy kết hợp Nginx và Apache

Trong mô hình **Reverse Proxy với Nginx và Apache**, Nginx hoạt động như một proxy ngược (reverse proxy) để chuyển tiếp các yêu cầu từ người dùng đến các ứng dụng web chạy trên Apache. Cả hai phần mềm này kết hợp với nhau để tận dụng được ưu điểm của từng phần mềm và tối ưu hóa hiệu suất của hệ thống.

### 1. Reverse Proxy với Nginx

Nginx hoạt động như một **Reverse Proxy** trong mô hình này. Khi người dùng gửi yêu cầu HTTP/HTTPS đến các domain như `wpadmin.nguyenbinh.site` hoặc `laravel.nguyenbinh.site`, Nginx sẽ tiếp nhận yêu cầu và chuyển tiếp chúng đến các port của Apache (ví dụ: 8080 cho HTTP và 8443 cho HTTPS), nơi các ứng dụng WordPress và Laravel đang chạy.

- **SSL/TLS Termination**: Nginx có thể xử lý việc giải mã SSL/TLS (mã hóa HTTPS) cho các kết nối đến, sau đó chuyển tiếp yêu cầu dưới dạng HTTP không mã hóa đến Apache. Điều này giúp giảm tải cho Apache và cải thiện hiệu suất hệ thống tổng thể.
  
**Lý do sử dụng Nginx làm Reverse Proxy**:
- **Hiệu suất cao**: Nginx có thể xử lý một lượng lớn yêu cầu đồng thời với tài nguyên hệ thống ít hơn so với Apache. Điều này rất hữu ích khi có lượng truy cập lớn và giúp tối ưu hóa khả năng mở rộng của hệ thống.
- **Xử lý tĩnh tốt hơn**: Nginx được tối ưu hóa để phục vụ các tệp tĩnh như hình ảnh, CSS, JavaScript rất nhanh chóng và hiệu quả, giúp giảm tải cho Apache.
  
### 2. Apache Web Server

Apache được cấu hình để phục vụ các ứng dụng web động như WordPress và Laravel. Apache được chọn vì nó hỗ trợ PHP tốt và có khả năng sử dụng các mô-đun như `mod_php` để xử lý các yêu cầu PHP.

**Lý do sử dụng Apache**:
- **Tương thích tốt với WordPress**: WordPress yêu cầu các tính năng đặc biệt của Apache như `.htaccess` và các mô-đun Apache để tối ưu hóa cấu hình và thực thi.
- **Xử lý PHP tốt**: Apache có thể dễ dàng xử lý các yêu cầu PHP nhờ vào `mod_php` hoặc sử dụng FastCGI để phục vụ các ứng dụng PHP như Laravel.
- **Cấu hình SSL trên Apache**: Apache xử lý kết nối HTTPS cho các ứng dụng chạy trên port 8443 khi người dùng truy cập qua HTTPS.

### 3. MySQL

MySQL được cài đặt để lưu trữ dữ liệu cho cả WordPress và Laravel. Mỗi ứng dụng sẽ có cơ sở dữ liệu riêng biệt (`wordpress_db` cho WordPress và `laravel_db` cho Laravel), với người dùng và quyền truy cập riêng.

### 4. Tạo Virtual Hosts và Cấu hình Apache/Nginx

- **Apache Virtual Hosts**: Được cấu hình cho từng domain (`wpadmin.nguyenbinh.site` và `laravel.nguyenbinh.site`), với các cổng HTTP (8080) và HTTPS (8443) riêng biệt.
- **Nginx Server Blocks**: Cấu hình trên Nginx để proxy yêu cầu tới các ứng dụng đang chạy trên Apache.

## Lý do sử dụng Nginx và Apache

### Ưu điểm của Nginx:

1. **Hiệu suất cao**: Nginx xử lý các kết nối đồng thời rất tốt nhờ vào mô hình bất đồng bộ (asynchronous), giúp giảm tải hệ thống khi có nhiều yêu cầu đồng thời.
2. **Xử lý các yêu cầu tĩnh tốt hơn**: Nginx được tối ưu hóa để phục vụ các tệp tĩnh (hình ảnh, CSS, JavaScript) nhanh chóng, giúp tiết kiệm băng thông và giảm thời gian tải trang.
3. **SSL/TLS Termination**: Nginx có thể chịu trách nhiệm giải mã SSL, giảm tải cho Apache và giúp tăng hiệu suất tổng thể.
4. **Cấu hình đơn giản**: Cấu hình của Nginx dễ hiểu và dễ bảo trì, đặc biệt khi làm reverse proxy hoặc load balancing.

**Nhược điểm của Nginx**:
- **Khó cấu hình cho ứng dụng động (như PHP)**: Nginx không thể xử lý PHP trực tiếp như Apache, nên cần cấu hình thêm FastCGI hoặc sử dụng Apache làm backend để xử lý PHP.
- **Hỗ trợ hạn chế đối với `.htaccess`**: Nginx không hỗ trợ `.htaccess` như Apache, điều này có thể gây khó khăn trong việc cấu hình cho các ứng dụng như WordPress.

### Ưu điểm của Apache:

1. **Hỗ trợ tốt với PHP**: Apache có khả năng xử lý các ứng dụng PHP như WordPress và Laravel nhờ vào `mod_php` hoặc FastCGI.
2. **Tính linh hoạt với `.htaccess`**: Apache hỗ trợ `.htaccess`, giúp quản trị viên dễ dàng cấu hình các thiết lập cho ứng dụng mà không cần thay đổi cấu hình toàn cục của máy chủ.
3. **Hỗ trợ mô-đun phong phú**: Apache có nhiều mô-đun để mở rộng chức năng, chẳng hạn như `mod_rewrite` để tạo các URL đẹp cho WordPress.

**Nhược điểm của Apache**:
- **Hiệu suất kém hơn so với Nginx**: Apache sử dụng mô hình đa tiến trình (multi-threaded), dẫn đến việc sử dụng tài nguyên nhiều hơn khi xử lý lượng yêu cầu lớn đồng thời.
- **Khó mở rộng**: Apache không có khả năng mở rộng tốt như Nginx khi cần xử lý một lượng lớn yêu cầu.

## Kết luận

Nginx được sử dụng làm **Reverse Proxy** để tận dụng khả năng xử lý tốc độ cao, ít tốn tài nguyên và khả năng xử lý SSL, trong khi Apache chịu trách nhiệm xử lý các ứng dụng PHP động như WordPress và Laravel, vì nó hỗ trợ PHP tốt hơn và có thể sử dụng `.htaccess` để cấu hình dễ dàng cho các ứng dụng.

Mô hình này kết hợp ưu điểm của cả hai phần mềm: Nginx xử lý các yêu cầu tĩnh và SSL, còn Apache chuyên xử lý các ứng dụng PHP động, giúp tối ưu hóa hiệu suất hệ thống và mở rộng dễ dàng.
