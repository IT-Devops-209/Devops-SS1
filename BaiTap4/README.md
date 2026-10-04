# Bài 4: Cấu hình tường lửa bảo vệ máy chủ (UFW & Cloud Firewall Integration)

## Mục tiêu
* Thiết lập tường lửa UFW (Uncomplicated Firewall) ngay trong hệ điều hành Ubuntu để lọc các gói tin mạng đi vào.
* Kết hợp cấu hình DigitalOcean Cloud Firewall ở tầng hạ tầng để bảo vệ máy chủ từ biên mạng trước khi gói tin chạm đến Droplet.

## Yêu cầu
**Bối cảnh:** Nhằm tránh máy chủ bị khai thác qua các cổng dịch vụ không sử dụng, bạn cần cấu hình tường lửa 2 lớp để chỉ cho phép lưu lượng SSH và HTTP đi vào Droplet.

**Ràng buộc:**
* **Lớp 1 (UFW trong OS):** Kích hoạt tường lửa UFW, thiết lập chặn mặc định lưu lượng đi vào (`default deny incoming`), cho phép lưu lượng đi ra ngoài (`default allow outgoing`). Mở cổng 22/tcp (SSH) và 80/tcp (HTTP).
* **Lớp 2 (DO Cloud Firewall):** Truy cập DigitalOcean Console, tạo một Cloud Firewall mới. Cấu hình Inbound Rules chỉ cho phép: SSH (cổng 22) và HTTP (cổng 80) từ mọi nguồn. Gán Droplet của bạn vào Cloud Firewall này.

## Kiểm tra
**Lệnh kiểm tra:**
* Trên Droplet, chạy lệnh: `sudo ufw status verbose` *(Yêu cầu: phải hiển thị trạng thái active và danh sách cổng cho phép).*
* Từ máy cá nhân, thử kết nối SSH và truy cập HTTP cổng 80 *(Yêu cầu: phải thành công).* 
* Thử ping hoặc quét thử một cổng khác không mở *(Yêu cầu: phải bị chặn/timeout).*

## Hướng dẫn nộp bài

### 1. Cấu hình UFW (Lớp 1)
Chạy các lệnh sau trên Droplet:
```bash
sudo ufw default deny incoming
sudo ufw default allow outgoing
sudo ufw allow 22/tcp
sudo ufw allow 80/tcp
sudo ufw enable
sudo ufw status verbose
```
**Kết quả log (Text output từ `sudo ufw status verbose`):**
*(Học viên dán text output của lệnh `sudo ufw status verbose` trên Droplet vào đây)*

### 2. Cấu hình DigitalOcean Cloud Firewall (Lớp 2)
*(Học viên đính kèm ảnh chụp màn hình thiết lập Cloud Firewall trên DigitalOcean Console hiển thị Inbound Rules tại đây)*
