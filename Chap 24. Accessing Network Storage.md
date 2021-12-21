- [1. NFS Services](#1)
  - [1.1 ](#11)
  - [1.2 ](#12)
- [2. CIFS Services](#2)
- [3. Mounting Remote File Systems Through fstab](#3)
- [4. Using Automount to Mount Remote File Systems](#3)
- [Tham khảo](#tm)

---



<a name ='1'></a>
# 1. NFS Services
- NFS - Network File System là một giao thức phân phối file system, nó cho phép bạn mount các thư mục từ xa có trên server.
- NFS được phát triển bởi SUN Microsystem, bắt đầu từ năm 1984 với phiên bản đầu tiên.
- Cho đến nay đã có tất cả 6 phiên bản:
  - version 1: phát hành năm 1984 với mục đích thí nghiệm
  - version 2: phát hành năm 1989, được đưa ra thị trường
  - version 3: phát hành năm 1995 với nhiều cải tiến
  - version 4 năm 2000, version 4.1 năm 2010 và version 4.2 năm 2016
- Cho phép bạn quản lý không gian lưu trữ ở một nơi khác và ghi vào không gian lưu trữ này từ nhiều clients.
- NFS cung cấp một cách tương đối nhanh chóng và dễ dàng để truy cập vào các hệ thống từ xa qua mạng và hoạt động tốt trong các tình huống mà các tài nguyên chia sẻ sẽ được truy cập thường xuyên.
- Dung lượng file mà NFS cho phép client truy cập lớn hơn 2GB, đòi hỏi hệ thống phải có phiên bản kernel lớn hơn hoặc bằng 2.4x và glibc từ 2.2.x trở lên
- Truyền thông giữa client và server thực hiện qua mạng Ethernet
- Client và Server sử dụng RPC (Remote Procedure Call) để giao tiếp với nhau.
- NFS sử dụng cổng 2049
- NFS hoạt động theo mô hình client/server. Một server đóng vai trò storage system, cho phép nhiều client kết nối tới để sử dụng dịch vụ.
- **NFS Security**
  - NFS giống như bất kỳ giao thức mạng không được bảo vệ nào khác dễ bị tấn công hai loại: nghe lén và tấn công kẻ mạo danh.
  - Một kẻ nghe trộm có thể thu thập dữ liệu trái phép vì nó đi qua mạng. Kẻ mạo danh có thể truy cập trái phép vào mạng





























