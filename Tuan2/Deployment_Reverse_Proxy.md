Dưới đây là hướng dẫn cấu hình **reverse proxy** cho hai website WordPress và Laravel sử dụng Nginx và Apache, PHP 8.1, MySQL và phpMyAdmin, với các domain là `wpadmin.nguyenbinh.site` và `laravel.nguyenbinh.site`. Mã cấu hình được viết trong file `.md` để bạn dễ dàng theo dõi và thực hiện.

# Hướng dẫn cấu hình Reverse Proxy cho 2 website WordPress và Laravel với Nginx và Apache

## 1. Cài đặt Apache

Cài đặt Apache:

```bash
sudo apt install apache2 -y
```

Kiểm tra trạng thái Apache:

```bash
sudo systemctl status apache2
```

## 2. Cài đặt PHP 8.1

Thêm repository và cài PHP 8.1 cùng các module cần thiết:

```bash
sudo add-apt-repository ppa:ondrej/php
sudo apt update
sudo apt install php8.1 php8.1-cli php8.1-common php8.1-mysql php8.1-xml php8.1-curl php8.1-mbstring php8.1-zip -y
```

Kiểm tra phiên bản PHP:

```bash
php -v
```

## 3. Cài đặt MySQL

Cài đặt MySQL Server:

```bash
sudo apt install mysql-server -y
```

Bảo mật MySQL:

```bash
sudo mysql_secure_installation
```

### Tạo cơ sở dữ liệu và người dùng MySQL:

```bash
sudo mysql -u root -p
```

Tạo cơ sở dữ liệu cho WordPress và Laravel:

```sql
CREATE DATABASE wordpress_db;
CREATE DATABASE laravel_db;
```

Tạo người dùng và cấp quyền:

```sql
CREATE USER 'wp_user'@'localhost' IDENTIFIED BY 'password';
CREATE USER 'laravel_user'@'localhost' IDENTIFIED BY 'password';
GRANT ALL PRIVILEGES ON wordpress_db.* TO 'wp_user'@'localhost';
GRANT ALL PRIVILEGES ON laravel_db.* TO 'laravel_user'@'localhost';
FLUSH PRIVILEGES;
EXIT;
```

## 4. Cài đặt phpMyAdmin

```bash
sudo apt install phpmyadmin -y
```

## 5. Thiết lập Virtual Hosts cho Apache

### Đổi port Apache từ 80 sang 8080:

Mở file `ports.conf` và chỉnh sửa:

```bash
nano /etc/apache2/ports.conf
```

Thêm dòng sau:

```apache
Listen 8080
```

Tạo cấu hình VirtualHost cho `wpadmin.nguyenbinh.site` (WordPress):

```bash
sudo nano /etc/apache2/sites-available/wpadmin.nguyenbinh.site.conf
```

Nội dung:

```apache
<VirtualHost *:8080>
    ServerName wpadmin.nguyenbinh.site
    DocumentRoot /var/www/wpadmin.nguyenbinh.site

    <Directory /var/www/wpadmin.nguyenbinh.site>
        AllowOverride All
        Require all granted
    </Directory>

    ErrorLog ${APACHE_LOG_DIR}/wpadmin_error.log
    CustomLog ${APACHE_LOG_DIR}/wpadmin_access.log combined
</VirtualHost>
```

Tạo cấu hình VirtualHost cho `laravel.nguyenbinh.site` (Laravel):

```bash
sudo nano /etc/apache2/sites-available/laravel.nguyenbinh.site.conf
```

Nội dung:

```apache
<VirtualHost *:8080>
    ServerName laravel.nguyenbinh.site
    DocumentRoot /var/www/laravel.nguyenbinh.site

    <Directory /var/www/laravel.nguyenbinh.site>
        AllowOverride All
        Require all granted
    </Directory>

    ErrorLog ${APACHE_LOG_DIR}/laravel_error.log
    CustomLog ${APACHE_LOG_DIR}/laravel_access.log combined
</VirtualHost>
```

Kích hoạt các Virtual Hosts:

```bash
sudo a2ensite wpadmin.nguyenbinh.site.conf
sudo a2ensite laravel.nguyenbinh.site.conf
sudo systemctl reload apache2
```

## 6. Cài đặt WordPress và Laravel

### Cài đặt WordPress:

Tải WordPress về:

```bash
cd /var/www/
sudo wget https://wordpress.org/latest.tar.gz
sudo tar -xvzf latest.tar.gz
sudo mv wordpress wpadmin.nguyenbinh.site
```

Điều chỉnh quyền sở hữu thư mục:

```bash
sudo chown -R www-data:www-data /var/www/wpadmin.nguyenbinh.site
```

### Cài đặt Laravel:

Cài đặt Composer (nếu chưa cài đặt):

```bash
sudo apt install curl php-cli php-mbstring git unzip -y
cd ~
curl -sS https://getcomposer.org/installer -o composer-setup.php
sudo php composer-setup.php --install-dir=/usr/local/bin --filename=composer
```

Tạo dự án Laravel:

```bash
cd /var/www/
sudo composer create-project --prefer-dist laravel/laravel laravel.nguyenbinh.site
```

Điều chỉnh quyền sở hữu thư mục:

```bash
sudo chown -R www-data:www-data /var/www/laravel.nguyenbinh.site
```

## 7. Cài đặt Nginx làm Reverse Proxy

Cài đặt Nginx:

```bash
sudo apt install nginx -y
```

Khởi động và kích hoạt Nginx:

```bash
sudo systemctl start nginx
sudo systemctl enable nginx
```

### Cấu hình Reverse Proxy cho Nginx:

Tạo file cấu hình cho `wpadmin.nguyenbinh.site` (WordPress):

```bash
sudo nano /etc/nginx/sites-available/wpadmin.nguyenbinh.site
```

Nội dung:

```nginx
server {
    listen 80;
    server_name wpadmin.nguyenbinh.site;

    location / {
        proxy_pass http://127.0.0.1:8080;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}
```

Tạo file cấu hình cho `laravel.nguyenbinh.site` (Laravel):

```bash
sudo nano /etc/nginx/sites-available/laravel.nguyenbinh.site
```

Nội dung:

```nginx
server {
    listen 80;
    server_name laravel.nguyenbinh.site;

    location / {
        proxy_pass http://127.0.0.1:8080;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}
```

Kích hoạt các cấu hình Nginx:

```bash
sudo ln -s /etc/nginx/sites-available/wpadmin.nguyenbinh.site /etc/nginx/sites-enabled/
sudo ln -s /etc/nginx/sites-available/laravel.nguyenbinh.site /etc/nginx/sites-enabled/
```

Kiểm tra cấu hình Nginx:

```bash
sudo nginx -t
```

Khởi động lại Nginx:

```bash
sudo systemctl restart nginx
```

## 8. Cài đặt SSL cho các domain

Cài đặt Certbot:

```bash
sudo apt install certbot python3-certbot-nginx -y
```

Cài đặt SSL cho `wpadmin.nguyenbinh.site`:

```bash
sudo certbot --nginx -d wpadmin.nguyenbinh.site
```

Cài đặt SSL cho `laravel.nguyenbinh.site`:

```bash
sudo certbot --nginx -d laravel.nguyenbinh.site
```

## 9. Kiểm tra và hoàn tất cấu hình

Kiểm tra lại các file cấu hình trong Apache và Nginx, đảm bảo rằng mọi cấu hình SSL đã được thiết lập đúng.

### Cấu hình trong Nginx:

```nginx
server {
    listen 443 ssl;
    server_name wpadmin.nguyenbinh.site;
    ssl_certificate /etc/letsencrypt/live/wpadmin.nguyenbinh.site/fullchain.pem;
    ssl_certificate_key /etc/letsencrypt/live/wpadmin.nguyenbinh.site/privkey.pem;
    include /etc/letsencrypt/options-ssl-nginx.conf;
    ssl_dhparam /etc/letsencrypt/ssl-dhparams.pem;
    location / {
        proxy_pass https://localhost:8443;
    }
}
```

### Cấu hình trong Apache:

```apache
<VirtualHost *:8443>
    ServerName wpadmin.nguyenbinh.site
    DocumentRoot /var/www/wpadmin.nguyenbinh.site
    SSLEngine on
    SSLCertificateFile /etc/letsencrypt/live/wpadmin.nguyenbinh.site/fullchain.pem
    SSLCertificateKeyFile /etc/letsencrypt/live/wpadmin.nguyenbinh.site/privkey.pem
</VirtualHost>
```

---

Với các bước trên, bạn đã thiết lập thành công một mô hình reverse proxy cho 2 website WordPress và Laravel với Nginx và Apache, sử dụng SSL cho các domain `wpadmin.nguyenbinh.site` và `laravel.nguyenbinh.site`.
```
