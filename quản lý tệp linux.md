#  Các thư mục trong linux
 
Sơ đồ thư mục hệ thống linux

![image](https://user-images.githubusercontent.com/92305335/139211765-d59d17ed-6e36-4f50-bfc7-df970d18d89a.png)

 
- / : 

  - Thư mục gốc, chưa tất cả file và thư mục hệ thống

  - Chỉ người dùng root mới có quyền ghi cho thư mục này

![image](https://user-images.githubusercontent.com/92305335/139211836-ee481bad-c4ec-4e2f-a0de-0f68949fe1bf.png)


- /boot: 

  - Chứa linux kernel, file ảnh hỗ trợ load hệ thống
 
 ![image](https://user-images.githubusercontent.com/92305335/139211889-cb55beb4-6cfe-4788-abbb-95da20f2bf99.png)


- /bin:

  - Chứa các tin nhị phân hỗ trợ việc boot và thi hành lệnh  
  
  ![image](https://user-images.githubusercontent.com/92305335/139216333-83068987-2500-4b0b-acd0-ad73a366aa5c.png)
 
- /dev: 

  - Chứa các tập tin thiết bị phần cứng, bao gồm các thiết bị đầu cuối, thiết bị được gắn vào hệ thống. Vd: cdrom, cpu, core… 
 
 ![image](https://user-images.githubusercontent.com/92305335/139216392-aaab20b9-1c8e-4f2b-a087-f7fbbb24cb5d.png)

- /etc: 

  - Chứa các file cấu hình yêu cầu bởi tất cả các chương trình

  - /etc kiểu soát cách hệ điều hành và hệ thống hoạt động
 
![image](https://user-images.githubusercontent.com/92305335/139216442-b4498362-9dce-4f4f-b8f5-654727ae8270.png)

- /home: 
  - Thư mục chính của người dùng, mỗi người dùng sẽ được tạo thư mục riêng và sử dụng
 ![image](https://user-images.githubusercontent.com/92305335/139216487-a2fa73e2-35da-4a3c-a957-cd3f55bdc84c.png)

- /lib, /lib64: 

  - Thứa các file thư viện chia sẻ cho các tệp tin nhị phân nằm dưới /bin và /sbin

  - Chứa thư viện dùng chung để khởi động hệ thống và chạy các lệnh trong hệ thống tệp gốc
![image](https://user-images.githubusercontent.com/92305335/139216512-a3168e36-1038-411d-899b-82bb89d4b1db.png)

 
- /media:

  - Thư mục chứa các mount tạm thời cho các thiết bị tháo lắp

	Vd: /media/cdrom cho CD-ROM; /media/floppy cho ổ đĩa mềm; /media/cdrecorder cho ổ đĩa ghi CD

- /mnt

  - Thư mục mount tạm thời nơi mà người quản trị hệ thống có thể mount các tập tin hệ thống.

- /opt

  - Chứa các ứng dụng thêm không thuộc hệ điều hành, các thư mục ứng dụng sẽ được lưu tại /otp.

Vd: viz, java 

- /proc: 

  - Chứa các thông tin về tiến trình hệ thống

  - Các tiến trình đang chạy sẽ được lưu thông tin tại đây. 

  - Đây là các tập tin hệ thống ảo với nội đung tài nguyên hệ thống
 ![image](https://user-images.githubusercontent.com/92305335/139216570-b073d928-fba8-4b96-a01c-6707bc7af998.png)

- /root:

  - Là thư mục của người dùng root

  - Chỉ người dùng root mới được sử dụng thư mục này 

- /run

  - Chứa dữ liệu của tiến trình chạy từ khi bắt đầu đến khi kết thúc

  - /run bao gồm tệp id và tệp khóa và một số thứ khác  
![image](https://user-images.githubusercontent.com/92305335/139216600-dd0d8068-cd0e-4bf4-b8fc-8246206a83c7.png)

- /sbin

  - Giống như /bin, chứa các tập tin nhị phân và  thi hành lệnh

  - Được dùng cho quản trị viên và bảo trì hệ thống

- /srv

  - Srv là viết tắt của service

  - Sử dụng cho các dịch vụ như NTS, HTTP,…

- /sys

  - Chứa các file giao diện phần cứng khác nhau và các tiến trình liên quan được quản lý bởi linux kernel và các tiến trình liên quan.
 ![image](https://user-images.githubusercontent.com/92305335/139216644-b678f678-c7d0-4f9f-81f3-94933ddc1970.png)

- /usr

  - Chứa đựng các thư mục con có tệp chương trình , thư viện cho các file chương trình và tài liệu về chúng ![image](https://user-images.githubusercontent.com/92305335/139216681-429ed21a-7dad-4389-9e4e-8364f7b5e561.png)
 
- /var

  - Chứa các file có thể thay đổi kích thước như log file, mail boxet, và spool files
 ![image](https://user-images.githubusercontent.com/92305335/139216701-330ee21d-019e-457a-baaa-8919ad13be90.png)

- /tmp

  - Thư mục chứa các tập tin tạm được tạo bởi hệ thống và người dùng
 
  - Các tập tin trong thư mục này bị xóa khi hệ thống khởi động lại.
# Tham khảo 

https://kb.hostvn.net/cau-truc-cay-thu-muc-trong-linux_61.html
