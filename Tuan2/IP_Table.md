# Tường lửa Iptables trên Linux và khả năng tích hợp mã hóa để bảo mật thông tin

## Giới thiệu về Iptables

Iptables là một công cụ tích hợp trong hệ điều hành Linux, thực hiện chức năng tường lửa theo cơ chế lọc gói (packet filtering). Ngoài ra, Iptables còn hỗ trợ chuyển đổi địa chỉ mạng (NAT - Network Address Translation) và thay đổi các thành phần của gói tin (packet mangling).

Iptables sử dụng cấu trúc bảng để định nghĩa các tập luật, bao gồm:

- **Các bảng (tables):**
  - `filter`: Xử lý việc lọc gói tin.
  - `nat`: Chuyển đổi địa chỉ mạng.
  - `mangle`: Thay đổi các thành phần của gói tin.

- **Các chuỗi (chains):**
  - `INPUT`: Xử lý gói tin đi vào hệ thống.
  - `OUTPUT`: Xử lý gói tin đi ra từ hệ thống.
  - `FORWARD`: Xử lý gói tin đi qua hệ thống.
  - `PREROUTING` và `POSTROUTING`: Dùng trong chuyển đổi địa chỉ và thay đổi gói tin.

- **Các luật (rules):** Xác định điều kiện và hành động đối với gói tin, như cho phép (ACCEPT), từ chối (DROP, REJECT) hoặc các tác động khác.

Ví dụ về một luật trong Iptables:

```bash
iptables -A FORWARD -d 192.168.1.1 -p tcp -j DROP
