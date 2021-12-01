# Mục lục 
- [1. Understanding LVM ](#1)
  - [1.1 LVM Architecture](#11)
  - [1.2LVM Features](#12)
- [2. Creating LVM Logical Volumes](#2)
  - [2.1 Creating the Physical Volumes](#21)
  - [2.2 Creating the Volume Groups](#22)
  - [2.3 Creating the Logical Volumes and File Systems](#23)
  - [2.4 Understanding LVM Device Naming](#24)
- [3. Resizing LVM Logical Volumes](#3)
  - [3.1 Resizing Volume Groups](#31)
  - [3.2 Resizing Logical Volumes and File Systems](#32)
- [4. Configuring Stratis](#4)
  - [4.1 Understanding Stratis Architecture](#41)
  - [4.2 Creating Stratis Storage](#42)
  - [4.3 Managing Stratis](#43)
- [5. Configuring VDO](#5)
  - [5.1 Understanding VDO](#51)
  - [5.2 Setting Up VDO](#52)

  --- 

<a name ='1'></a>
# 1. Understanding LVM

- Việc xử lý storage bằng cách phân vùng trên disk  vẫn tồn tại nhược điểm và nó không linh hoạt. 
- Logical Volume Manager (LVM) : LVM là kỹ thuật quản lý việc thay đổi kích thước lưu trữ của ổ cứng. Là một phương pháp ấn định không gian ổ đĩa thành những logical volume khiến cho việc thay đổi kích thước của một phân vùng trở nên dễ dàng 
- Một số khái niệm khác: 
  - Physical volume: Một ổ đĩa vật lý có thể phân chia thành nhiều phân vùng vật lý gọi là Physical Volumes.
  - Volume group: Là một nhóm bao gồm nhiều Physical Volume trên 1 hoặc nhiều ổ đĩa khác nhau được kết hợp lại thành một Volume Group
  - Logical volume: Một Volume Group được chia nhỏ thành nhiều Logical Volume. Nó được dùng cho các để mount tới hệ thống tập tin (File System) và được format với những chuẩn định dạng khác nhau như ext2, ext3, ext4…

<a name = '11'></a>
## 1.1 LVM Architecture

- Trong kiến trúc LVM, một số layer có thể đk phân biệt. Trong layer thấp nhất, thiết bị lưu trữ được sử dụng. 

- Các thiết bị lưu trữ cần được gắn cờ(flag) như physical volumes, nó cho phép chúng có thể sử dụng trong môi trường LVM và làm cho chúng có thể sử dụng được bởi các tiện ích khác đang cố gắng truy cập vào logical volume

- Các layer của LVM 
  - Tầng đầu tiên : hard drives là tầng các disk ban đầu khi chưa chia phân vùng
  - Partitions: Sau đó ta chia các disk ra thành các phân vùng nhỏ hơn
  - Physical volume : từ một partitions ta sẽ tạo ra được một physical
  - Group volume : Ta sẽ ghép nhiều physical volume thành một group volume
  - Logical volume : Ta sẽ có thể tạo ra được logical volume
- Một thiết bị lưu trữ là một khối vật lý có thể thêm đến volume group. Đó là tính trừu tượng (abstraction) của tất cả các bộ nhớ có sẵn. Abstraction có nghĩa là volume group không phải thứ cố định, có thể thay đổi khi cần thiết, nó giúp thêm nhiều không gian trên cấp độ volume group khi sắp hết dung lượng ổ đĩa. Tức khi hết không gian disk trên một logical volume, sẽ có dung lượng có sẵn từ volume group, nếu không có dung lượng có sẵn trên volume group thì chúng sẽ được thêm bởi physical volume. 

- Ở đầu volume group là logical volume. Logic không hoạt động trực tiếp trên đĩa nhưng lấy dung lượng đĩa từ dung lượng đĩa có sẵn trên volume group. Logical volume bao gồm bộ nhớ có sẵn từ nhiều physical volume, 

- Các file hệ thống thực tế được tạo trên volume group, logical volume linh hoạt với kích thước. Nếu một file hệ thống sắp hết không gian ổ đĩa, nó tương đối dễ dàng để mở rộng file hệ thống hoặc để giảm bộ nhớ nếu file hệ thống cho phép. 

- Tổng quan kiến trúc LVM 
  ![image](image/Screenshot_136.png)

<a name = '12'></a>
## 1.2 LVM Features

- LVM cung cấp một giải pháp linh hoạt để quản lý lưu trữ, volume không còn bị ràng buộc đến những hạn chế của ổ cứng vật lý
- Nếu cần thêm dung lượng, volume group đễ dàng mở rộng bằng cách thêm một plysical volume mới, vì vậy dung lượng đĩa có thể được thêm đến logical  volume. 
- Có thể giảm kích thước của một logical nhưng chỉ khi nếu file hệ thống được tạo  trên volume hỗ trợ tính năng giảm kích thước hệ thống
- LVM hỗ trợ snapshot giúp trở lại trường hợp trước đó hoặc sao lưu hệ thống trên logical volume
  - LVM snapshot được tạo bằng cách copy dữ liệu quản trị logical volume  mô tả trạng thái hiện tại của file đến snapshot volume.
  - Snapshot sẽ thay đổi khi file nguyên gốc volume thay đổi, khi lập kết hoạch cho snapshot nên chắc chắn dung lượng ổ đĩa có sẵn. 

-  LVM logical volumes có thể thay thế phần cứng lỗi dễ dàng. Nếu phần cứng bị lỗi, dững liệu có thể được di chuyến ra ngoài volume group (thông qua lệnh pvmove) ổ đĩa lỗi có thể được xóa khỏi volume group  và một đĩa cứng mới có thể thêm vào một cách linh hoặ mà không cân thời gian chết nào cho chính logical volume 

<a name ='2'></a>
# 2. Creating LVM Logical Volumes

- Tạo LVM  logical volume liên quan đến việc tạo layer 3 trong kiến trúc LVM
  - Đầu tiên phải chuyển đổi các thiết bị vật lý vào volume physical(PVs)
  - Tiếp theo tạo volume group(VG) và gán PVs cho nó  
  - Cuối cùng, tạo logical volume(LV) chính.

<a name ='21'></a>
## 2.1 Creating the Physical Volumes

- Tạo một phân vùng với type là LVM. 
  ![image](image/Screenshot_139.png)

- Tạo physical volume 
  ![image](image/Screenshot_140.png)

- Nhập `pvs` để xác định pv đã được tạo
  ![image](image/Screenshot_141.png)

- Nhập `pvdisplay` để hiển thị thêm nhiều thông tin
  ![image](image/Screenshot_142.png)
  
- Nhập `lsblk  ` để xem tổng quát về cấu hình lưu trữ hiện tại của sever.
  ![image](image/Screenshot_143.png)
   










Tham khảo 

https://blog.cloud365.vn/linux%20tutorial/tong-quan-lvm/

https://vinasupport.com/lvm-la-gi-tao-vao-quan-ly-logical-volume-manager/
