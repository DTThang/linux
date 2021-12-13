# Mục lục 
- [1. Hardening the SSH Server](#1)
  - [1.1 Limiting Root Access](#11)
  - [1.2 Configuring Alternative Ports](#12)
  - [1.3 Modifying SELinux to Allow for Port Changes](#13)
  - [1.4 Limiting User Access](#14)
- [2. Using Other Useful sshd Options](#2)
  - [2.1 Session Options](#21)
  - [2.2 Connection Keepalive Options](#22)
- [3. Configuring Key-Based Authentication with Passphrases](#3)

---

<a name ='1'></a>
# 1. Hardening the SSH Server

- SSH giúp thiết lập kết nối từ xa tới server. Nó là một giải pháp thuận tiện nhưng cũng là một giải pháp nguy hiểm. 
- Hacker sẽ cố gắng tấn công các máy chủ ssh qua port 22 và thông qua các tài khoản root bằng thuật toán đoán password.
- Một số biện pháp để ngăn chăn tấn công qua ssh.
  - Vô hiệu hóa đăng nhập root
  - Vô hiệu hóa mật khẩu root
  - Cấu hình port nondefault cho ssh lắng nghe
  - Chỉ định người đùng được phép ssh 

<a name ='11'></a>
## 1.1 Limiting Root Access
- Sửa đổi tham số PermitRootLogin trong file /etc/ssh/sshd_config để vô hiệu hóa đăng nhập root
- Sau khi thiết lập restart lại service
  

<a name ='12'></a>
## 1.2 Configuring Alternative Ports

- Có tất cả 65535 port có khả năng lắng nghe. Kẻ tấng công có thể quét tất cả các công hoặc tập trung vào các port đã biết, và ssh port 22 luôn nằm trong các cổng này
- Có thể thay đổi port 22 bằng một port khác để để lắng nghe ssh. Có thể chọn một port ngẫu nhiên hoặc port 443
- Port 443 theo mặc định được gán cho web server sử dụng TLS (Transport Layer Security) để cung cấp mã hóa.  
- Nếu người dùng muốn truy cập vào máy chủ SSH thường đứng sau một proxy chỉ cho phép truy cập đến các cổng 80 và 443, thì việc định cấu hình SSH để lắng nghe trên cổng 443 có thể có ý nghĩa.
- Một port chỉ có thể lắng nghe một service tại một thời điểm 
  ![image](image/chap20/Screenshot_1.png)    
















