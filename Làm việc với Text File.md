# Mục lục
- [1. Sử dụng câu lệnh đọc](#1)
- [2. Sử dụng lệnh grep](#2)
- [Tham khảo](#tm)
 
---
<a name = '1'></a>
## 1. Sử dụng các câu lệnh đọc
- more 
  - Dùng mở một tệp để đọc tương tác
  - Vd: Đọc file /etc/passwd bằng lệnh more

![image](https://user-images.githubusercontent.com/92305335/139472891-72e4b2c5-e47c-45d0-af6c-5279413c76dd.png)

- less
  - Mở văn bản trong một trang, dễ đọc
  - Vd: Đọc file /etc/passwd bằng lệnh less

![image](https://user-images.githubusercontent.com/92305335/139472985-d82a77f2-595a-45ef-a61b-0232f6205e7d.png)


- cat
  - Xuất nội dung văn bản lên màn hình, đọc nhiều file cùng lúc 
  - Đọc nội dung tệp file1

![image](https://user-images.githubusercontent.com/92305335/139473306-5ea7371f-1e0b-425b-90c2-5ec96e52249a.png)

- head
  - Hiển thị 10 dòng đầu của văn bản 

  - Cú pháp `head [tuỳ chọn] file`

tùy chọn | mô tả 
----|----
-n, --lines=[-]n| In số dòng n đầu tiên của mỗi tệp
-c, --byte=[-]n| In số byte(ký tự) n đầu tiên của mỗi tệp
-q| Không in tiêu đề xác định tên tệp
-v| Luôn in tiêu đề xác định tên tệp

  - Vd: 

    - In 5 dòng đầu của /etc/passwd

`head -n 5 /etc/passwd`

![image](https://user-images.githubusercontent.com/92305335/139466483-8305295c-0235-4721-8927-576f098a4aa7.png)

- tail

  - Hiển thị 10 dòng cuối của văn bản 

  - Cú pháp `tail [tuỳ chọn] file`

 tùy chọn | mô tả
---- | ----
-n number| In số dòng number cuối cùng của mỗi tệp
-n +number| In tất cả các dòng từ number về sau
-c | In số byte n đầu cuối cùng mỗi tệp
-q| Không in tiêu đề đầu ra
-f| Tiếp tục đọc tập tin cho đến khi CTRL + C

Vd

- In 9 dòng cuối của /etc/passwd:  `tail -n 9 /etc/passwd`



![image](https://user-images.githubusercontent.com/92305335/139468146-add0baf0-62f9-4b4a-9f2c-e89336bc9f43.png)

- In từ dòng thứ 16 trở đi của /etc/passwd: `tail -n +16 /etc/passwd`

![image](https://user-images.githubusercontent.com/92305335/139468256-910d266b-b96a-4531-b498-ed8c9da21de9.png)

- sort

  - Sắp xếp nội dung của một văn bản 

cú pháp | mô tả 
----|----
sort file | sắp sếp các dòng theo thứ tự ở đầu dòng 
sort -r file | sắp xếp các dòng theo thứ tự ngược lại 
sort -k file| chỉ định cột được sắp xếp  

Vd

- Sắp xếp /etc/passwd: `sort /etc/passwd`

![image](https://user-images.githubusercontent.com/92305335/139469848-8dcacdf1-71be-4109-8afe-ba5314c58dab.png)

- Sắp xếp ngược lại: `sort -r /etc/passwd`

![image](https://user-images.githubusercontent.com/92305335/139470032-ca4311c6-5f0a-430f-9310-0e9922b79c2a.png)

- wc 

  - Đếm số lượng dòng, chữ và kí tự của văn bản
  - Vd: Hiển thị dòng, chữ ký tự của /etc/passwd

` wc /etc/passwd` 

![image](https://user-images.githubusercontent.com/92305335/139472270-c8d47822-3648-4d71-8286-7e14fa563272.png)

<a name = '2'></a>
# 2.Sử dụng lệnh grep

  - Cú pháp `grep [tuỳ chọn] <file>`
  - Hiển thị dòng chứa chuỗi ký tự trong file, hay nhiều file,  có thể thay file bằng đường dẫn


lệnh|mô tả
---| ---
grep [pattern] <filename>	|Tìm kiếm một pattern trong một tệp và in tất cả các dòng khớp
grep -v [pattern] <filename>	|In tất cả các dòng không khớp với pattern
grep [0-9] <filename>	|In các dòng có chứa các số từ 0 đến 9
grep -r [pattern] | Tìm kiếm [pattern] trong cả thư mục hiện tại và thư mục con 
grep -i [pattern] | tìm kiếm [pattern] cả chữ hoa và chữ thường
grep -A [number] [pattern] | In các dòng và số dòng sau pattern phù hợp
grep -B [number] [pattern] | In các dòng và số dòng trước pattern phù hợp
  
  
Vd
  
  - In dòng có ký tự Ins trong file2: `grep Ins file2`

![image](https://user-images.githubusercontent.com/92305335/139477246-8ef4af56-e045-44af-88ee-93ae3318cd05.png)

  - In dòng không có ký tự Ins trong file2: `grep -v Ins file2`

![image](https://user-images.githubusercontent.com/92305335/139477418-30b34e2c-3ab8-4937-98c2-1879d3313e50.png)

  - In dòng có ký tự từ a-c trong file2: `grep [a-c] file2`

![image](https://user-images.githubusercontent.com/92305335/139477610-54aa1f87-9d19-49e2-9fc8-0ca2f8d8cd0d.png)

  - In các dòng chứa Ins và 1 dòng sau đó: `grep -A1 Ins file2`

![image](https://user-images.githubusercontent.com/92305335/139479116-07c83dbf-2872-4af8-bc9d-2bd573b7549b.png)
  
  <a name = 'tm'></a>
  # Tham khảo

https://blogd.net/linux/cach-dung-lenh-sort-uniq-paste-join-split/#2-l%E1%BB%87nh-sort3

https://blogd.net/linux/cach-su-dung-head-tail-less-more/#2-1-l%E1%BA%B9-nh-head

https://blogd.net/linux/lenh-grep-toan-tap/
