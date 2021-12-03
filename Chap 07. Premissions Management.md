# Mục Lục
- [1. Quản lý quyền sở hữu tệp](#1)
- [2. Quyền quản lý cơ bản](#2)
- [3. Quyền quản lý nâng cao](#3)
- [Tham khảo](#tm) 



<a name ='1'></a>
# 1. Quản lý quyền sở hữu tệp 
- Hiển thị quyền: ls -l 

![image](https://user-images.githubusercontent.com/92305335/139529681-19aa0c1f-2533-4eb4-8ff7-e21c090b612b.png)

- Tổng quát về phân quyền trong linux 

![image](https://user-images.githubusercontent.com/92305335/139573840-8dbf6507-7083-455e-b1ef-3b58fef21dbc.png)

  - Vd: 

![image](https://user-images.githubusercontent.com/92305335/139574004-9a80994b-f7d5-4300-8284-c7b067ccaea9.png)

file type| user |group| orther | name
---|---|---|---|---
-|rw-|r--|r--| ten_file.tar.gz
d|rwx|r-x|r-x| toan

ký hiệu | ý nghĩa 
---|---
d| thư mục
-|file
r|đọc 
w| ghi 
x| thực thi
-| không có quyền

<a name ='2'></a>
# 2. Quyền quản lý cơ bản
- chown 
   - Thay đổi quyền sở hữu file, thư mục

  `chown [option]... [tên user][:[tiên group]] tệp/thư mục`

Thay đổi quyền sở hữu của thư mục toan thành người dùng user2 và nhóm group2 

`chown user2:group2 toan`

![image](https://user-images.githubusercontent.com/92305335/139573456-7418e63c-7e62-43be-a499-04bd25939eec.png)

Thay đổi quyền sở hữu của thư mục toan và cả tệp/thư mục conthành người dùng user3 và nhóm group4

![image](https://user-images.githubusercontent.com/92305335/139573538-8db3d569-e87e-49dd-ae75-fdec5cf6d278.png)

  - `chown -R` hoạt động trong tệp/thư mục một cách đệ quy
     
- Có thể dùng lệnh chgrp để thay đổi nhóm của tệp/thư mục

- chmod
  - Dùng để thay đổi quyền của một tệp/thư mục 
  - Phân quyền bằng số 
    - Cấu trúc lệnh `chmod <permissions-number> <filename>`

![image](https://user-images.githubusercontent.com/92305335/139574618-b083a3c9-335c-4280-9992-830872495730.png)

- Permissions -number về cơ bản sẽ có 3 chữ số một số với ý nghĩa số thứ nhất là quyền của user, số thứ 2 là quyền của group, số thứ 3 là quyền của other

Số	|Ký hiệu|	Ý nghĩa
---|---|---
0	|---|	Không có quyền
1	|--x|	Thực thi
2	|-w-|	Ghi
3	|-wx|	Thực thi + Ghi
4	|r--|	Đọc
5	|r-x|	Đọc + Thực thi
6	|rw-|	Đọc + Ghi
7	|rwx|	Đọc + Ghi + Thực thi

- Giả sự file1 có quyền rwxr-xr-- có nghĩa user có đủ cả 3 quyền đọc, ghi thực thi, group có 2 quyền đọc và thực thi, other chỉ có quyền đọc

user: r + w +x = 4 +2+1=7

group: r + x = 4+1 =5

other: r = 4

Quyền của file sẽ là 754

Sử dụng lệnh để phân quyền  `chmod 754 file1`

Ngoài ra có thể sử dụng lệnh `chmod u+rwx,g+rw,o+r <filename>` để phân quyền 

- Sử dụng newgrp để thay đổi nhóm chính cho đến khi thoát lệnh và log out


<a name ='3'></a>
## 3. Các quyền quản lý nâng cao
  - Có 3 quyền nâng cao là: 
    - SUID
    - SGID
    - Sticky bit

    
Quyền| Mô tả
--- | ---
SUID|SUID hay Set user ID, được sử dụng trên các file thực thi (executable files) để cho phép việc thực thi được thực hiện dưới owner của file thay vì thực hiện như user đang loggin trong hệ thống. SUID cũng có thể được sử dụng để thay đổi ownership của files được tạo hoặc di chuyển nó đến một thư mục mà owner của nó sẽ là owner của thư mục chuyển đến thay vì là owner nó được tạo ra
SGID|SGID hay Set group ID, cũng tương tự như SUID, được sử dụng trên các file thực thi (executable files) để cho phép việc thực thi được thực hiện dưới owner group của file thay vì thực hiện như group đang loggin trong hệ thống. SGID cũng có thể được sử dụng để thay đổi ownership group của files được tạo hoặc di chuyển nó đến một thư mục mà owner group của nó sẽ là owner group của thư mục chuyển đến thay vì là group nó được tạo ra.
Sticky bit|Được sử dụng cho các thư mục chia sẻ, mục đích là ngăn chặn việc người dùng này xóa file của người dùng kia. Chỉ duy nhất owner file (và root) mới có quyền rename hay xóa các file, thư mục khi nó đã được set sticky bit. sticky bit được môt tả bằng chữ cái “t” ở dòng cuối cùng của hiển thị permission.

- Gán quyền SUID, SGID, stick bit

Quyền | Giá trị số| Giá trị tương đối |Trên tệp| Trên thư mục
--- |---| ---|---| ---
SUID| 4| u+s|Người dùng thực thi tệp với sự cho phép của chủ sở hữu tệp |Không có  
SGID| 2 |g+s| Người dùng thực thi với sự cho phép của chủ sở hữu nhóm| Các tệp được tạo trong thư mục có cùng chủ sở hữu nhóm
Sticky bit| 1| +t |Không có | Ngăn chặn người dùng này xóa tệp của người dùng khác 

Vd:
- Cấp quyền SUID cho file1 `chmod 4754 file1` hoặc ` chmod u+s file1`

![image](https://user-images.githubusercontent.com/92305335/139709017-b0a45df6-cd02-499e-8bdb-97af64b9174c.png)

- Để xóa quyền SUID,GUID, stick bit 

 SUID | GUID | stick bit
---|--- | ---
chmod u-s | chmod g-s | chmod -t 

<a name ='tm'></a>
#Tham khảo: 

https://viblo.asia/p/phan-quyen-trong-linux-yMnKMbDNZ7P

https://1hosting.com.vn/chmod-va-sticky-bits-tren-linux/
