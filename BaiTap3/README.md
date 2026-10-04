# Bài 3: Cài đặt Nginx và cấu hình Website tĩnh cơ bản (Basic Nginx Web Server)

## Mục tiêu
* Cài đặt dịch vụ Web Server Nginx trên hệ điều hành Ubuntu Server thông qua trình quản lý gói `apt`.
* Thiết lập một Server Block tùy chỉnh lắng nghe trên cổng mặc định HTTP (80) để phục vụ một trang HTML tĩnh của dự án.

## File nộp bài
* `index.html`: File mã nguồn tĩnh.
* `ptit-web.conf`: File cấu hình Server Block của Nginx.

## Các lệnh thực hiện trên VPS (Tham khảo):

```bash
# 1. Cài đặt Nginx
sudo apt update
sudo apt install nginx -y

# 2. Tạo thư mục chứa mã nguồn
sudo mkdir -p /var/www/ptit-web/html

# Phân quyền cho thư mục
sudo chown -R $USER:$USER /var/www/ptit-web/html
sudo chmod -R 755 /var/www/ptit-web

# 3. Tạo file cấu hình Server Block (Copy ptit-web.conf vào)
sudo nano /etc/nginx/sites-available/ptit-web.conf

# 4. Kích hoạt Server Block và hủy kích hoạt cấu hình mặc định (default)
sudo ln -s /etc/nginx/sites-available/ptit-web.conf /etc/nginx/sites-enabled/
sudo rm /etc/nginx/sites-enabled/default

# 5. Kiểm tra cú pháp và khởi động lại Nginx
sudo nginx -t
sudo systemctl reload nginx
```
