 # Mục Lục
- [1. Giới thiệu](#1)
- [2. User](#2)
- [3. Group](#3)
 
 
 <a name ='1'></a>
# 1. Giới thiệu
- Trong linux có 2 loại người dùng:
  - Người dùng không có quyền đặc biệt: user1, user2
  - Người dùng có quyền đặc biệt, mặc định là root
- Người dùng root toàn quyền truy cập vào mọi thứ trên linux và làm việc không giới hạn trong không gian hệ thông. Điều này người dùng bình thường không làm được  

![image](https://user-images.githubusercontent.com/92305335/139522379-c4afbb38-801b-4da9-a276-84eca7fa32b9.png)

- Làm việc với  root
  - su: cho phép chạy lệnh với người dùng thay thế và ID nhóm
  - sudo: cho phép người dùng chạy lệnh với quyền root mà không cần phải chuyển sang chế độ root


 <a name ='2'></a>
# 2.User
 
- Thông tin tài khoản user được lưu trong /etc/passwd

![image](https://user-images.githubusercontent.com/92305335/139522989-493c3d03-8050-4736-ab3c-c16a13c4f787.png)


![image](https://user-images.githubusercontent.com/92305335/139522931-b6b02bc1-3af5-46e9-bb54-53cb5a25ed55.png)

  - Mỗi user có đặc điểm sau: 
    - Tên tài khoản là duy nhất
    - Mỗi user có 1 mã định danh duy nhất (UID)
    - Một user có thể thuộc nhiều group
- Thông tin mật khẩu của user được lưu trong /etc/shadow, chỉ có root mới truy cập vào được tệp tin này  

![image](https://user-images.githubusercontent.com/92305335/139523074-0c9fe41f-14ec-4bf7-95ef-0e93d77e8fc0.png)

![image](https://user-images.githubusercontent.com/92305335/139523146-3cf10475-b9ba-4002-a283-9d5a2b400018.png)

- Tạo user
  - Lệnh useradd tạo tài khoản người dùng mới
 `useradd [option] name-user`

lựa chọn| mô tả 
---|---
-c| tạo bí danh.
-u| thiết lập user ID. Mặc định sẽ lấy số ID tiếp theo để gán cho user.
-d| chỉ định thư mục home.
-g| chỉ định nhóm chính.
-G| chỉ định nhóm phụ (nhóm mở rộng).
-s| chỉ định shell cho user sử dụng.

Vd: Tạo người dùng user3 với UID = 466 và GID là 1000

`useradd -u 466 -g 1000 user3`

![image](https://user-images.githubusercontent.com/92305335/139524053-9f9a980b-b256-4951-b7e1-f081a5c6640f.png)

- Lệnh usermod: chỉnh sửa thông tin tài khoản 
  - Cấu trúc lệnh: `usermod [option] name-user`

lựa chọn |mô tả 
---|---
-c| tạo bí danh.
-u| thiết lập user ID. Mặc định sẽ lấy số ID tiếp theo để gán cho user.
-d| chỉ định thư mục home.
-g| chỉ định nhóm chính.
-G| chỉ định nhóm phụ (nhóm mở rộng).
-s| chỉ định shell cho user sử dụng
-L| khóa tài khoản 
-U| mở khóa tài khoản

- Lệnh passwd: tạo, thay đổi mật khẩu cho user

  - Cấu trúc lệnh: `passwd name-user`

  - Cài password cho người dùng trong khoảng thời gian tối thiểu 30 ngày, hết hạn sau 90 ngày và có 3 ngày cảnh cáo trước khi hết hạn

![image](https://user-images.githubusercontent.com/92305335/139524979-a261ba0a-80e9-4f20-a4b4-a2dc773571d6.png)


- Lệnh chage: thay đổi thông tin mật khẩu cho user

  - Cấu trúc lênh: `chage [options] name-user`

lựa chọn |mô tả
--- | ---
-l | xem chính sách của 1 user
-E| thiết lập ngày hết hạn cho account. Vd: chage -E 08/17/2020 vdn178
-I| thiết lập số ngày bị khóa sau khi hết hạn mật khẩu
-m| thiết lập số ngày tối thiểu được phép thay đổi password
-M| thiết lập số ngày tối đa được phép thay đổi password
-W| Thiết lập số ngày cảnh báo trước khi hết hạn mật khẩu.

- Lệnh userdel để  xóa user: `userdel name-user`

<a name = '3'></a>
# 3. Group

- Nhóm là nhóm tập hợp nhiều user. Mỗi nhóm có tên duy nhât, mã định danh (GID) duy nhất.

- Thông tin tài khoản group được lưu trong /etc/group

![image](https://user-images.githubusercontent.com/92305335/139525244-1e8e8374-c090-4a58-9d7c-60a91679b016.png)

- Thông tin tài khoản group được lưu trong /etc/gshadow

- Lệnh groupadd: tạo nhóm mới  
  - Cấu trúc lệnh: `groupadd [option] name-group`

  - Để gán GID cho groud ta dùng `groupadd -g name-group`	

  - Tạo nhóm group1 với GID là 500: `groupadd -g 500 group1`

![image](https://user-images.githubusercontent.com/92305335/139525755-ccc161d1-4e3a-44e3-b15b-a91e9e7b4b6d.png)

- Lệnh groupmod: chỉnh sửa thông tin nhóm 

lựa chọn| mô tả
---|---
groupmod -g  | sửa GID của nhóm
groupmod -n | sửa tên nhóm 

  - Sửa nhóm group1 thành group2 và thay đổi GID thành 600

![image](https://user-images.githubusercontent.com/92305335/139525903-ca6f9b2d-8267-4793-a9ca-7176fbff9a35.png)


- Lệnh groupdel: xóa nhóm 
  - Cấu trúc lệnh: `groupdel name-group`

- lệnh vipw, vigr
  -  Cấu trúc `vipw [option]

  -  Lệnh vipw and vigr dùng để sửa file trong /etc/passwd và /etc/group
  -  Với option -s, ta có thể sửa file trong /etc/shadow và /etc/gshadow
