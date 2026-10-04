# Bài 1: Khởi tạo Droplet trên DigitalOcean

## Mục tiêu
* Thực hành đăng ký tài khoản, lựa chọn cấu hình phần cứng phù hợp và khởi tạo thành công Droplet chạy hệ điều hành Ubuntu Server trên hạ tầng đám mây DigitalOcean.
* Cấu hình xác thực an toàn bằng cặp khóa SSH (SSH Keypair) thay vì mật khẩu thô và thực hiện kết nối thành công từ máy cá nhân.

## Yêu cầu
**Bối cảnh:** Nhóm DevOps của bạn cần tạo một máy chủ thử nghiệm trên hạ tầng đám mây DigitalOcean để chuẩn bị chạy các dự án Web.

**Ràng buộc:**
* Tạo Droplet chạy hệ điều hành Ubuntu 22.04 LTS (hoặc bản mới nhất).
* Lựa chọn cấu hình tối giản tiết kiệm chi phí: Basic plan, Regular SSD, CPU Shared (loại rẻ nhất, ví dụ: $4/tháng hoặc $6/tháng).
* Chọn datacenter region gần Việt Nam nhất (Singapore).
* Tại mục Authentication, bắt buộc chọn SSH Keys. Tạo mới một cặp khóa SSH từ máy cá nhân của bạn, thêm khóa công khai (Public Key) vào tài khoản DigitalOcean và gán vào Droplet khi khởi tạo.
* Kết nối thành công tới Droplet thông qua SSH từ máy tính cá nhân bằng tài khoản mặc định root.

## Kiểm tra
**Lệnh kiểm tra:** Chạy lệnh SSH từ Terminal máy cá nhân:
```bash
ssh -i /path/to/private_key root@<IP_ADDRESS_DROPLET>
```

**Kết quả mong đợi:** Truy cập thành công vào giao diện dòng lệnh của Droplet mà không cần nhập mật khẩu. Terminal hiển thị thông tin chào mừng của Ubuntu Server.

## Hướng dẫn nộp bài
*Cập nhật ảnh chụp màn hình hoặc log kết nối SSH thành công tại đây.*
