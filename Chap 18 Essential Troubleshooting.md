# Mục lục 
- [1. Understanding the RHEL 8 Boot Procedure](#1)
- [2. Passing Kernel Boot Arguments](#2)
  - [2.1 Accessing the Boot Prompt](#21)
  - [2.2 Starting a Troubleshooting Target](#22)
- [3. Using a Rescue Disk](#3)
  - [3.1 Restoring System Access Using a Rescue Disk](#31)
  - [3.2 Reinstalling GRUB Using a Rescue Disk](#32)
  - [3.3 Re-Creating the Initramfs Using a Rescue Disk](#33)
- [4. Fixing Common Issues](#4)
  - [4.1 Recovering from File System Issues](#41) 
  - [4.2 Resetting the Root Password](#42)  
- [5. Recovering Access to a Virtual Machine](#4)
- [Tham khảo](#tm)
---



<a name ='1'></a >
# 1. Understanding the RHEL 8 Boot Procedure
- Khi sự cố khởi động xảy ra cần phải đáng giá gian đoạn nào của quá trình xảy ra sự cố và sự  dụng công cụ thích hợp đê khắc phục sự cố.
- Tóm tắt thủ tục khởi động trên linux
  - 1. Performing POST: Khi nguồn máy mở. Từ firmware hệ thống có thể là UEFI hoặc BIOS Power-On Self-Test (POST) được thực thi, và phần cứng yêu cầu để khởi động hệ thống được khởi tạo.
  - 2. Selecting the bootable device: từ UEFI boot firmware hoặc từ BIOS, một thiết bị có khả năng khởi động được đặt.
  - 3. Loading the boot loader: từ bootable device, một boot loader được đặt. Trong RHEL, thường sử dụng GRUB 2
  - 4. Loading the kernel: Boot loader trình bày một menu boot cho người dùng hoặc có thể cấu hình để tự động bắt đầu mặc định hệ điều hành. Để load linux, kernel được tải cùng với initramfs. Initramfs bao gồm bao gồm kernel module cho tất cả phần cứng được yêu cầu để boot cũng như các tập lệnh ban đầu cần thiết để tiến hành giai đoạn khởi động tiếp theo.
  - 5. Starting /sbin/init: khi kernel được tải vào bộ nhớ, process đầu tiên trong tất cả được load, nhưng vẫn từ initramfs. Đó là process /sbin/init mà trong RHEL được liên kết đến Systemd. Demon udev được load để quan tâm đến quá trình khởi tạo hơn  nữa. Tất cả đều xảy ra từ initramfs image
  - 6. Processing initrd.target: Systemd process thực thi tất cả unit từ initrd.target cái mà chuẩn bị cho môi trường vận hành tối thiểu, nơi mà file hệ thông root trên ổ đĩa được gắn trên thư mục /sysroot. Lúc này, đã đủ được tải để chuyển đến cài đặt hệ thống được ghi vào ổ cứng
  - 7. Switching to the root file system: hệ thống chuyển đổi đến hệ thống file rootrên ổ đĩa và thời điểm này có thể load Systemd process từ đĩa tốt hơn 
  - 8. Running the default target: systemd tìm target default để thực thi và chạy tất cả các unit trong đó. Trong process này màn hình đăng nhập được bày ra và người dùng có thể xác thực. Lời nhắc đăng nhập có thể xuất hiện trước khi các systemd unit được load thành công. Do đó việc nhắc đăng nhập không có nghĩa hệ thống đã hoạt động hoàn toàn. 

- Trong mỗi giai đoạn một số vấn đề có thể xảy ra do cấu hình sai hoặc một số thứ khác. Bảng dưới tóm tắt một số thứ ta có thể làm khi gặ vấn đề ở một giai đoạn cụ thể


  Boot phase | Configuring It | Fixing It
  ---|---|---
  POST | Cấu hình phần cứng (F12, Esc, F10 hoặc ký tự khác ) | Thay thế ổ cứng 
  Selecting the bootable device | Cấu hình BIOS/UEFI hoặc menu boot ổ cứng | Thay thế ổ cứng hoặc sử dụng hệ thống cứu trợ 
  Loading the boot loader | grub2-install và chỉnh sửa đến file /etc/defaults/grub | Nhắc khởi động GRUB và chỉnh sửa  đến /etc/defaults/grub bằng cách sử dụng grub2-mkconfig 
  Loading the kernel | Chỉnh sửa đến cấu hình GRUB và /etc/dracut.conf | Nhắc khởi động GRUB và chỉnh sửa đến /etc/defaults/grub bằng cách dùng grub2-mkconfig
  Starting /sbin/init | Tổng hợp thông tin initrams | Đối số khởi động **init= kernel**, đối số khởi động kernel **rd.break**
  Processing initrd.targe | Tổng hợp thông tin initrams | Thường không bắt buộc 
  Switch to the root file system | Chỉnh sửa đến file /etc/fstab |Chỉnh sửa đến file /etc/fstab 
  Running the default target | Dùng systemctl set -default để tạo sysbolic link /etc/systemd/system/default.target | Bắt đầu rescue.target nhưu một đối số boot kernel


<a name ='2'></a >
# 2. Passing Kernel Boot Arguments
 
<a name ='21'></a>
## 2.1 Accesing the boot prompt
- Trong menu khi khởi động do GRUB cung cấp nhập e để để mở chế độ có thể chỉnh sửa lệnh hoặc c để vào GRUB command prompt đầy đủ. để truyền các option boot đến kernel đang khởi động nhâp e. Việc chỉnh sửa ở đây chỉ có tác dụng một lần  
  ![image](image/chap18/Screenshot_1.png)



<a name ='22'></a>
## 2.2 Starting a Troubleshooting Target
- Nếu gặp sự cố khi khởi động máy củ, có một số option  có thể nhập vào trong GRUB boot prompt
  - **rd.break** dừng quá trình khởi động trong khi vẫn đang ở trong giai đoạn initramfs.. Tùy chọn này hữu ích nếu không có mật khẩu root có sẵn. 
  - **init=/bin/sh or init=/bin/bash** điều này chỉ định một shell nên bắt đầu ngay sau khi tải xong kernel và initrd. Điều này hữu ích nhưng không phải sự lựa chọn tốt nhất vì một vài trường hợp sẽ mất đi một số chức năng khác.
  - **systemd.unit=emergency.target** điều này chuyển sang chế độ tải số lượng systemd unit tối thiểu 
  - **systemd.unit=rescue.target** điều này bát đầu thêm một số systemd unit  để mang lại một chế độ hoạt động hoàn chỉnh. Điều này yêu cầu pass root. Dùng `systemctl list-units` để xem số lượng file unit được load 

Ví dụ: nhập `systemd.unit=rescue.target` vào cuối dòng linux$(root)/vmlinuz và bắt đầu hệ thống. 
  ![image](image/chap18/Screenshot_2.png)
  ![image](image/chap18/Screenshot_4.png)



<a name ='3'></a>
# 3. Using a Rescue Disk

<a name ='31'></a>
## 3.1 Restoring System Access Using a Rescue Disk

  ![image](image/chap18/Screenshot_5.png)

- **Install Red Hat Enterprise Linux 8 in Basic Graphics Mode** Đặt lại máy. Không sử dụng nếu muốn khắc phục sự cố một tình huống bình thường không hoạt động  và cần một chế độ đồ họa cơ bản.
-  **Rescue a Red Hat Enterprise Linux System** Nó linh hoạt nhất trong hệ thống cứu hộ.
- **Run a Memory Test** Chạy tùy chọn này nếu bộ nhớ bị lỗi. Nó cho phép đánh dấu  chíp bộ nhớ  vì vậy máy có thể khởi động bình thường.
- **Boot from Local Drive** Nếu không thể boot từ GRUB trên ổ đĩa cứng, hãy thử  option này trước. Nó cung cấp một boot loader cố gắng để cài từ ổ ứng của máy , như vậy đây là option có sẵn ít xâm nhập nhất.

- Khi bắt đầu cứu hộ một hệ thống, cầ bật quyền truy cập đầy đủ vào ổ đĩa trên đĩa cài đặt. Thông thường đĩa cứu hộ cài đặt và gắn nó vào thư mục /mnt/sysimage. DÙng `chroot /mnt/sysimage` để lấy nội dung thư mục này làm môi trường làm việc thực tế. Nếu không sử dụng chroot một số tiện ích sẽ không hoạt động.

  - Khởi động máy và chọn Troubleshooting
  ![image](image/chap18/Screenshot_6.png)    

  - Chọn Rescue a Red Hat Enterprise Linux System
  ![image](image/chap18/Screenshot_8.png)    

  - Hệ thống cứu hộ hiện đã nhắc bạn rằng nó sẽ cố gắng tìm một linux được cài đặt hệ thống và gắn trên /mnt/sysimage nhập 1 để tiếp tục
  - Nếu cài đặt Red Hat hợp lệ đã được tìm thấy, bạn sẽ được nhắc rằng hệ thống của bạn có được gắn dưới /mnt/sysimage. Tại thời điểm này, bạn có thể nhấn Enter hai lần để truy cập vỏ cứu hộ
  ![image](image/chap18/Screenshot_9.png)
  - Nhập chroot /mnt/sysimage. Tại thời điểm này ta có quyền truy cập vào hệ thống tệp tin gốc và có thẻ truy cập tất cả các công cụ để sửa chữa quyền truy cập vào hệ thống. 
  - Nhập exit và reboot để khởi động lại máy ở chế độ bình thường  

<a name ='32'></a>
## 3.2 Reinstalling GRUB Using a Rescue Disk

- Các bước cài lại GRUB2 
  - Cài đặt môi trường làm việc chroot /mnt/sysimage 
  ![image](image/chap18/Screenshot_10.png)

  - Dùng lệnh `grub2-install [name device]`, với KVM  `grub2-install /dev/vda`, với `VMware grub2-install /dev/sda`



<a name ='33'></a>
## 3.3 Re-Creating the Initramfs Using a Rescue Disk

- Khi image intramfs bị hỏng, sẽ không thể khởi động vào server ở chế độ bình thường
- Để sửa chữa image intramfs sau khi khởi động vào môi trường cứu hộ, sử dụng lênh `dracut`. Khi chạy mỗi lệnh riêng nó sẽ tạo ra mội initramfs mới cho kernel hiện đang tải 

- File cấu hình với tên /etc/dracut.conf có các tùy chọn cụ thể trong kh tạo lại các initramfs 
- Cầu hình dracut phân tán ở các vị trí  
  - /usr/lib/dracut/dracut.conf.d/*.conf bao gồm các file cấu hình mặc định
  - /etc/dracut.conf.d chứa các file cấu hình dracut tùy chỉnh 
  - /etc/dracut.conf được sử dụng làm file cấu hình chính  

<a name ='4'></a>
# 4. Fixing Common Issues

<a name ='41'></a>
## 4.1 Recovering from File System Issues




<a name ='41'></a>
## 4.2 Resetting the Root Password
- 1. Mở boot system nhập e khi vào menu boot
  ![image](image/chap18/Screenshot_11.png)

- 2. Nhập rd.break  như một đối số khởi động vào dòng tải kernel. Crtl-X để khởi động option này. Điều này sẽ đưa đến cuối của giai đoạn khởi động, nơi initramfs được load, ngay trước khi mount mộtt file root hệ thống trên thư mục /
  ![image](image/chap18/Screenshot_12.png)

- 3. Nhập `mount -o remount,rw /sysroot` để đọc/ghi  truy cập đến đến system image

- 4. Tại thời điểm này, nhập `chroot /sysroot` để tạo nội dung của thư mục /sysimage  thư mục root mới 
- 5. Nhập passwd để thiết lập lại pass cho root
  ![image](image/chap18/Screenshot_13.png)

- 6. Nhập `load_policy -i` để load SElinux policy
  ![image](image/chap18/Screenshot_14.png)

- 7. Nhập `chcon -t shadow_t /etc/shadow` để đặt ngữ cảnh chính xác đến /etc/shadow
  ![image](image/chap18/Screenshot_13.png)

- 8. Reboot hệ thống

<a name ='5'></a>
# 5. Recovering Access to a Virtual Machine




