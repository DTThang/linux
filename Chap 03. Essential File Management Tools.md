# Mục Lục 
- [1. Các thư mục trong linux](#1)

- [2. Mount](#2)

- [3. Quản lý tệp](#3)

- [4. Sử dụng liên kết](#4)

  - [1. Inode](#Inode)
  
  - [2. Hard links](#hard)
  
  - [3. Symbolic links](#sys) 
  
  - [4. Archives and compressed file](#arc)
  
[Tham khảo](#tm)


<a name = '1'></a>
#  1.Các thư mục trong linux
 
**Sơ đồ thư mục hệ thống linux**

![image](image/Screenshot_61.png)

- /  

  - Thư mục gốc, chưa tất cả file và thư mục hệ thống

  - Chỉ người dùng root mới có quyền ghi cho thư mục này

![image](https://user-images.githubusercontent.com/92305335/139211836-ee481bad-c4ec-4e2f-a0de-0f68949fe1bf.png)


- /boot 

  - Chứa linux kernel, file ảnh hỗ trợ load hệ thống
 
 ![image](https://user-images.githubusercontent.com/92305335/139211889-cb55beb4-6cfe-4788-abbb-95da20f2bf99.png)


- /bin

  - Chứa các tin nhị phân hỗ trợ việc boot và thi hành lệnh  
  
  ![image](https://user-images.githubusercontent.com/92305335/139216333-83068987-2500-4b0b-acd0-ad73a366aa5c.png)
 
- /dev 

  - Chứa các tập tin thiết bị phần cứng, bao gồm các thiết bị đầu cuối, thiết bị được gắn vào hệ thống. Vd: cdrom, cpu, core… 
 
 ![image](https://user-images.githubusercontent.com/92305335/139216392-aaab20b9-1c8e-4f2b-a087-f7fbbb24cb5d.png)

- /etc 

  - Chứa các file cấu hình yêu cầu bởi tất cả các chương trình

  - /etc kiểu soát cách hệ điều hành và hệ thống hoạt động
 
![image](https://user-images.githubusercontent.com/92305335/139216442-b4498362-9dce-4f4f-b8f5-654727ae8270.png)

- /home 
  - Thư mục chính của người dùng, mỗi người dùng sẽ được tạo thư mục riêng và sử dụng
 ![image](https://user-images.githubusercontent.com/92305335/139216487-a2fa73e2-35da-4a3c-a957-cd3f55bdc84c.png)

- /lib, /lib64 

  - Thứa các file thư viện chia sẻ cho các tệp tin nhị phân nằm dưới /bin và /sbin

  - Chứa thư viện dùng chung để khởi động hệ thống và chạy các lệnh trong hệ thống tệp gốc
![image](https://user-images.githubusercontent.com/92305335/139216512-a3168e36-1038-411d-899b-82bb89d4b1db.png)

 
- /media

  - Thư mục chứa các mount tạm thời cho các thiết bị tháo lắp

	Vd: /media/cdrom cho CD-ROM; /media/floppy cho ổ đĩa mềm; /media/cdrecorder cho ổ đĩa ghi CD

- /mnt

  - Thư mục mount tạm thời nơi mà người quản trị hệ thống có thể mount các tập tin hệ thống.

- /opt

  - Chứa các ứng dụng thêm không đi kèm theo hệ điều hành, các thư mục ứng dụng sẽ được lưu tại /otp.

Vd: viz, java 

- /proc 

  - Chứa các thông tin về tiến trình hệ thống

  - Các tiến trình đang chạy sẽ được lưu thông tin tại đây. 

  - Đây là các tập tin hệ thống ảo với nội đung tài nguyên hệ thống
 ![image](https://user-images.githubusercontent.com/92305335/139216570-b073d928-fba8-4b96-a01c-6707bc7af998.png)

- /root

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




<a name = '2'></a>
# 2. Mount
- mount, umount
  - Lệnh mount dùng để đính kèm tệp hệ thống được tìm thấy trên một số thiết bị vào ây tệp lớn
  - Lệnh umount dùng để tách nó ra một lần nữa
- Lệnh df -Th được đăng ký để hiển thị không gian nhớ khả dụng trong thiết bị được mount, nó bao gồm tất cả các mount hệ thống
![image](https://user-images.githubusercontent.com/92305335/139286330-786fbf67-723b-45e1-bb29-91b5c745ae05.png)
  - Tùy chọn  -h để tóm tắt kết quả đầu ra để ta có thể đọc
  - Tùy chọn -T hiển thị loại tệp hệ thống 
    - *Filesystem*: tên file  của thiết bị được tương tác với thiết bị đĩa  
    - *Type*: loại tệp hệ thống được sử dụng 
    - *Size*: kích thước của thiết bị được mount
    - *Used*: không gian đĩa của thiết bị được sử dụng 
    - *Avail*: không gian đĩa khả dụng
    - *Mounted on*: thư mục lưu trữ hiện tại 
- findmnt
  - Lệnh findmnt hiển thị các mount và các quan hệ tồn tại giữa các mount khác nhau
![image](https://user-images.githubusercontent.com/92305335/139288365-d8b05865-f2f8-4256-857f-eab67195d6d3.png)

<a name = '3'></a>
# 3. Quản lý tệp
- Wildcard
 
|Wildcard	 |  Ý nghĩa|
|---- | ----|
|   *  |  match bất kỳ ký tự nào|
|?  |  match 1 ký tự bất kỳ|
|[characters]  |  match ký tự nào có trong set|
| [!characters]  |  không match ký tự nào có trong set|
|[[:class:]] |    match ký tự định nghĩa bởi class|

- Lệnh ls
   - Được sử dụng để hiển thị danh sách tệp tin 

Lệnh   |  miêu tả     
------ | ------
ls -l | hiển thị danh sách dài, chứa thông tin về thuộc tính tệp
ls -a | hiển thị tất cả file, kể cả file ẩn 
ls -R | hiển thị thư mục và cả các tệp con
ls -S | hiển thị danh sách theo kích thước 
ls -s | hiển thị tệp cùng với dung lượng của tệp 
ls -t | hiển thị danh sách sắp xếp theo thời gian tạo

**ls -l**

![image](https://user-images.githubusercontent.com/92305335/139299768-b7cadf13-7136-4e35-b920-bf45aec5fdef.png)

**ls -a**

 ![image](https://user-images.githubusercontent.com/92305335/139299478-807d8626-23b0-4b7f-8c20-334d91b48f82.png)

**ls -R**

![image](https://user-images.githubusercontent.com/92305335/139299645-ebaaf88e-f494-417d-8baa-748f2ae4ba67.png)

- Lệnh copy  

  - Cấu trúc lệnh `cp [options] sourcefiles destdir`
  - Được sử dụng để copy file

lệnh | miêu tả
---- | ----
cp -a | lưu trữ
cp -f | sao chép đè lên tệp đích nếu cần  
cp -i  | hỏi trước ghi đè khi thư mục đích đã tồn tại file
cp -l | liên kết tệp thay vì sao chép 
cp -n | không ghi đè tệp
cp -R |sao chép thư mục một cách đệ quy

Vd: 

  - Copy f2 vào thư mục tm1

`cp f2 tm1` 

  - Copy tệp f1 trong tm1 đến tm2

`cp tm1/f1 tm2`

![image](https://user-images.githubusercontent.com/92305335/139386878-06def02b-09a6-4b59-ba3c-ffdaee1d8848.png)

  - Copy tất cả thư mục tm2 vào thư mục tm1 

`cp -R tm1 tm2`

![image](https://user-images.githubusercontent.com/92305335/139387042-cde3c266-d7ea-4dba-9ef5-ddec7e83a2c1.png)

  - Copy file2 vào tm1 và hỏi trước nếu file2 đã tồn tại trong tm1

`cp -i file2 tm1`

![image](https://user-images.githubusercontent.com/92305335/139386654-2d79de8e-0dcd-4acc-96fc-4a7bef3bd380.png)

  - Buộc copy tệp file2 vào thư mục tm3

`cp -f file2 tm3`

![image](https://user-images.githubusercontent.com/92305335/139388059-fa9fbe3c-22ab-4461-9d9c-7890731ebfe0.png)

  - Copy tất cả file bắt đầu bằng a vào thư mục  tm2

`cp *a tm2`

![image](https://user-images.githubusercontent.com/92305335/139388570-d6d8f653-2a5e-4d7b-bb85-7a32e7bb57e3.png)

- Moving

Cấu trúc lệnh: 

`mv [options] sourcefiles destdir`

  - Dùng để di chuyển tệp, thư mục

  - Dùng để đổi tên tệp, thư muc

Lệnh | mô tả
----|----
mv -f | buộc di chuyển bằng cách ghi đè tệp đích mà không có lời nhắc
mv -i | lời nhắc tương tác trước khi ghi đè
mv -u | cập nhật - di chuyển khi nguồn mới hơn đích

  - Đổi tên thư mục tm1 thành tm6

`mv tm1 tm6`

![image](https://user-images.githubusercontent.com/92305335/139390339-93573031-6189-408e-872a-ec01b08b922f.png)

  - Di chuyển thư mục tm3 vào thư mục tm2

`mv tm3 tm2`

![image](https://user-images.githubusercontent.com/92305335/139390686-dafbef2c-6b28-443a-9a32-7e48a261ccae.png)

- Delete

  - Cấu trúc lệnh: 

`rm [options] files destdir`

lệnh  | mô tả 
----|----
rmdir [tên thư mục]	|  Xóa thư mục rỗng
rm -rf [tên thư mục]	|  Xóa thư mục có dữ liệu

<a name = '4'></a>
# 4. Sử dụng liên kết
 
**Giới thiệu**: 

- Một liên kết là một kết nối giữa file name và dữ liệu thực tế trên ổ đĩa  
- Có 2 loại liên kết: hard link và symbolic 

<a name = 'Inode'></a>
## 1. Inode

- Trong Linux, dữ liệu của các file được chia thành các block. Có nhiều cách tổ chức để liên kết các khối dữ liệu trong một file với nhau, một trong các cách đó là dùng chỉ mục (indexed allocation).

![image](https://user-images.githubusercontent.com/92305335/139395361-dd438a40-45d0-4bfc-aa22-5e45cbbd30aa.png)

- Trong một inode cso các metadata sau:
  - Dung lượng file tính bằng byte.
  - Device ID: id của thiết bị lưu trữ file.
  - User ID: id của chủa chủ sở hữu file.
  - Group ID: id của nhóm sở hữu file.
  - File mode : gồm kiểu file và cách thức truy cập file.
  - Timestamps: các mốc thời gian khi: bản thân inode bị thay đổi (ctime, inode change time), nội dung file thay đổi (mtime, modification time) và lần truy cập mới nhất (atime, access time).
  - Link count : số lượng hard links trỏ đến inode. Các con trỏ chỉ đến các blocks trên ổ cứng dùng lưu nội dung file. Các con trỏ cho biết file nằm ở đâu để đọc nội dung.
- Inode xác định file và thuộc tính của nó. Mỗi inode được xác định bởi một con số duy nhất trong hệ thống tệp tin.
- Inote là một cấu trucs dữ liệu trong hệ thống tệp truyền thống của ho nhà unix như UFS hoặc EXT3. Inode lưu trữ thông tin về 1 tệp thông thường, thư mục hay những đói tượng khác của hệ thống tệp tin.
- Chú ý:
  - Inote ko chứa tên file, thư mục.
  - Các con trỏ là thành phần quan trọng nhất: nó cho biết địa chỉ các block lưu nội dung file và tìm đến các block đó có thể truy cập được nội dung file.

<a name = 'hard'></a>
## 2. Hard links

- Hard links là các liên kết cấp thấp ( low-level links) mà hệ thống sử dụng để tạo các thành phần của chính hệ thống file, chẳng hạn như file và thư mục. Liên kết cứng sẽ tạo một liên kết trong cùng hệ thống tập tin với 2 inode entry tương ứng trỏ đến cùng một nội dung vật lý (cùng số inode vì chúng trỏ đến cùng dữ liệu).
- Tất cả các hệ thống tệp tin dựa trên thư mục phải có ít nhất một liên kết cứng (link counts từ 1 trở lên) cung cấp tên gốc cho mỗi tệp tin

![image](https://user-images.githubusercontent.com/92305335/139396493-50da4e67-7453-430b-a5c8-9b95e5399d72.png)

- Lệnh tạo liên kết cứng như sau: `ln [file nguồn] [file đích]`

![image](https://user-images.githubusercontent.com/92305335/139399541-33ef85d4-962c-4a84-93f2-b1bfe268d4d3.png)

![image](https://user-images.githubusercontent.com/92305335/139399808-219901ab-46c6-46ea-ae6d-d933f360c669.png)

- 2 file viblo.txt và hardlink có cùng số inode là 136. Khi file gốc viblo.txt bị xóa thì nội dụng file hardlink.txt vẫn còn nguyên.

- Khi sử dụng lệnh rm để xóa file thì làm giảm đi một hard link. Khi số lượng hard link giảm còn 0 thì không thể truy cập tới nội dung của file được nữa

<a name = 'sys'></a>
## 3. Symbolic links
- Symbolic links là một file đặc biệt trỏ đến một file hoặc thư mục khác - được gọi là target. Khi được tạo, một symbolic links có thể được sử dụng thay cho target file. Nó có thể có một tên độc nhất, và được đặt trong bất kỳ thư mục nào. Nhiều symbolic links thậm chí có thể được tạo cho cùng một target file, cho phép truy cập target bằng nhiều tên khác nhau.
 
![image](https://user-images.githubusercontent.com/92305335/139400583-b8cd8ede-99da-4180-811f-8d7048a2757a.png)

- Symbolic link không chứa bản sao dữ liệu của target file. Nó tương tự như một shortcut trong Microsoft Windows: nếu bạn xóa một symbolic link, target sẽ không bị ảnh hưởng. Vì chỉ đơn thuần là một shortcut, symbolic link không dùng đến inode entry. Nó sẽ tạo ra một inode mới và nội dung của inode này trỏ đến tên tập tin gốc.

- Ngoài ra, nếu target của một symbolic link bị xóa, di chuyển hoặc đổi tên, symbolic link không được cập nhật. Khi điều này xảy ra, liên kết tượng trưng được gọi là "broken" hoặc "orphaned" và sẽ không còn hoạt động như một liên kết.

- Lệnh tạo liên kết tượng trưng như sau: `ln -s [file nguồn] [file đích]`

![image](https://user-images.githubusercontent.com/92305335/139401455-c551b762-7c3b-45ef-90ef-8a6fcffede54.png)

- 2 file viblo2.txt và sym-links.txt có số inode là khác nhau. Khi xóa file viblo2.txt thì nội dung của sum-links.txt sẽ bị mất

- Lệnh ls -l sẽ hiện thị tệp nào là symbolic link, nếu tệp tin là hard links thì sẽ hiển thị chỉ số inode giống nhau 

![image](https://user-images.githubusercontent.com/92305335/139403806-5916371a-39cf-4365-a6f4-433a300047fb.png)

![image](https://user-images.githubusercontent.com/92305335/139403836-c4340105-9b41-4334-a87c-4840eecda8b7.png)

<a name = 'arc'></a>
## 4. Archives and compressed file

- Cấu trúc lệnh: `tar -[option] file_archive files/directories`

option | mô tả
----|----
c| Tạo file lưu trữ.
x| Giải nén file lưu trữ.
z| Nén với gzip - Luôn có khi làm việc với tập tin gzip (.gz).
j| Nén với bunzip2 - Luôn có khi làm việc với tập tin bunzip2 (.bz2).
lzma| Nén với lzma - Luôn có khi làm việc với tập tin LZMA (.lzma).
f| Chỉ đến file lưu trữ sẽ tạo - Luôn có khi làm việc với file lưu trữ.
v| Hiển thị những tập tin đang làm việc lên màn hình.
r| Thêm tập tin vào file đã lưu trữ.
u| Cập nhật file đã có trong file lưu trữ.
t| Liệt kê những file đang có trong file lưu trữ.
delete| Xóa file đã có trong file lưu trữ.
totals| Hiện thỉ thông số file tar
exclude |loại bỏ file theo yêu cầu trong quá trình nén

Vd:
  - Tạo file nen1.tar lưu trữ các tập tin file1 file và các thư mục tm1 tm2

`tar -cvf nen1.tar tm1 file1 tm2 file2` 

![image](https://user-images.githubusercontent.com/92305335/139535613-f094b53e-303e-43ef-89e2-7ae0d9a11bbb.png)

  - Hiển liệt kê các file trong nen1.tar và các thông tin chi tiết

![image](https://user-images.githubusercontent.com/92305335/139535828-d4158ed0-4156-41d5-9bc0-1f5b9c1f2f15.png)

  - Để giảm dung lượng file, tạo file nén gzip nen1.tar.gz(nen1.tgz) lưu trữ các tập tin file1 file và các thư mục tm1 tm2

`tar -czvf nen1.tar tm1 file1 tm2 file2`

![image](https://user-images.githubusercontent.com/92305335/139536952-6877f601-1c12-4987-938c-3ce308e6731c.png)

![image](https://user-images.githubusercontent.com/92305335/139537340-3c3894ab-6489-468f-ab7b-1dab7c34f255.png)

  - Xóa file1 và file2 trong nen1.tar 

`tar -f nen1.tar --delete file1 file2`

![image](https://user-images.githubusercontent.com/92305335/139539387-680ccbc2-318f-4330-9144-6d881accb623.png)

  - Giải nén nen1.tar (thêm -z nếu là file gz, -j nếu là file bunzip): `tar -xf nen1.tar`

![image](https://user-images.githubusercontent.com/92305335/139539890-cd13ef71-e08f-4b20-946a-1ecbd5441c7f.png)

  - Giải nèn nen1.tar vào thư mục tm3 ta dùng option -C  `tar -xf nen1.tar -C tm3`

![image](https://user-images.githubusercontent.com/92305335/139541648-b46a2894-f3be-415e-bbea-c5c2248aeac1.png)

Ngoài `tar` còn có lênh `zip`, `gzip` để nén dữ liệu 

<a name = 'tm'></a>
# Tham khảo 

https://kb.hostvn.net/cau-truc-cay-thu-muc-trong-linux_61.html

https://www.rapidtables.org/vi/code/linux/cp.html

https://viblo.asia/p/hard-links-va-symbolic-links-tren-linux-07LKXJR2lV4

https://hocvps.com/nen-va-giai-nen-file-tar-gzip-va-zip/
