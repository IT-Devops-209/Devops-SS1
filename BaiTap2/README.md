# Bài 2: Khởi tạo User thường và thiết lập đặc quyền quản trị (Sudoers Configuration)

## Mục tiêu
* Tạo một tài khoản người dùng thường (Non-root user) trên Ubuntu Server để hạn chế rủi ro khi thao tác trực tiếp bằng quyền root tối cao.
* Cấp đặc quyền quản trị an toàn cho user thường thông qua nhóm sudo và sao chép cấu hình SSH Key để đăng nhập.

## Yêu cầu
**Bối cảnh:** Vận hành hệ thống theo nguyên tắc đặc quyền tối thiểu (Least Privilege), bạn cần tạo tài khoản làm việc riêng có tên là `devops` để thực hiện cấu hình máy chủ hàng ngày thay vì dùng `root`.

**Ràng buộc:**
* Tạo tài khoản người dùng mới tên là `devops` trên Droplet.
* Thêm user `devops` vào nhóm quản trị sudo.
* Sao chép cấu hình SSH Key từ thư mục của root sang thư mục home của user `devops` để cho phép tài khoản này đăng nhập được qua SSH.
* Phân quyền chính xác cho thư mục `.ssh` và file `authorized_keys` của user `devops` để cơ chế bảo mật SSH hoạt động.

## Kiểm tra
**Lệnh kiểm tra:**
1. Thực hiện đăng nhập từ máy cá nhân: 
```bash
ssh -i /path/to/private_key devops@<IP_ADDRESS_DROPLET>
```
*(Yêu cầu: Phải kết nối thành công)*

2. Sau khi đăng nhập, chạy lệnh:
```bash
sudo whoami
```
*(Yêu cầu: Yêu cầu nhập mật khẩu hoặc hiển thị kết quả là `root` thành công)*

**Kết quả mong đợi:** Đăng nhập thành công và thực thi được lệnh `sudo` mà không gặp lỗi phân quyền.

## Hướng dẫn nộp bài
*Học viên điền các lệnh Linux đã sử dụng và cập nhật log hiển thị từ terminal khi kiểm tra kết nối SSH.*

### Các lệnh thực hiện (Tham khảo):
```bash
# 1. Tạo user devops
adduser devops

# 2. Thêm devops vào nhóm sudo
usermod -aG sudo devops

# 3. Sao chép SSH Key cho devops và cập nhật owner
rsync --archive --chown=devops:devops ~/.ssh /home/devops/
```

### Log kiểm tra kết nối:
```bash
$ ssh -i ~/.ssh/id_ed25519 devops@103.72.57.95
Welcome to Ubuntu 22.04.3 LTS (GNU/Linux 5.15.0-84-generic x86_64)

devops@ubuntu-s-1vcpu-1gb-sgp1-01:~$ sudo whoami
[sudo] password for devops:
root
devops@ubuntu-s-1vcpu-1gb-sgp1-01:~$ 
```
