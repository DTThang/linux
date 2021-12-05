# Mục lục
- [1. Các nguyên tắc cơ bản](#1)
- [2. Quản lý giao diện và địa chỉ mạng](#2)
- [3. Xác thực cấu hình mạng](#3)
  - [1.Xác định cấu hình địa chỉ mạng](#31)
  - [2.Xác thực định tuyến](#32)
  - [3. Xác thực khả dụng của port và server](#33)
- [4. Cấu hình mạng với lệnh nmtui và nmcli](#4)
  - [1. Quyền yêu cầu thay đổi cấu hình mạng](#41)
  - [2. Cấu hình mạng với nmcli](#42)
  - [3. Cấu hình mạng với mntui](#43)
- [5. Cài Hostname và Name Resolution](#5)
- [Tham khảo](#tm)
<a name = '1'></a>
# 1. Các nguyên tăc cơ bản
- Có 2 loại địa chỉ IP (Internet Protocol) :
  - IPv4: là địa chỉ cơ sở có 32 bit gồm 4 nhóm hệ thập phân, được phân tách nhau bởi dấu chấm. Vd 192.168.47.133
  - IPv6: là địa chỉ cơ sở có 128 bit biểu diễn bởi 8 nhóm hệ hecxa được phân tách nhau bởi dấu ":". Vd: fe80:badb:abe01:45bc:34ad:1313:6723:8798

- Địa chỉ IP cần để các thiết bị kết nối với mạng bên ngoài.
- Để truy cập ra bên ngoài, mọi máy tính cần có 1 địa chỉ IP duy nhất.
- **Địa chỉ mạng riêng**
  - Là địa chỉ sử dụng cho mạng nội bộ
  - Một vài địa chỉ IP được chia ra theo mục địch:  
      - A Class A network: 10.0.0.0/8
      - 16 Class B network: 172.16.0.0/12
      - 256 Class C network: 192.168.0.0/16

- **NAT**
  -  NAT (Net Work Address Translation) thông thường được sử dụng cho router 
  - Trong NAT các nodes sử dụng địa chỉ IP riêng nhưng khi sử dụng mạng, địa chỉ Ip riêng này sẽ đợc thay thế bằng địa chỉ IP của NAT router. 
  - NAT router cho phép theo dõi tất cả các kết nối tồn tại cho phần máy chủ trong mạng.

- **Network Masks**
  - *Subnet mask* xác định trong địa chỉ ip phần nào là mạng, phần nào là nút
  - Vd: 192.168.10.100/24 với 3 bit đầu 192.168.10 là phần mạng và bit cuối 100 chỉ máy chủ trên mạng
  - Trong địa chỉ quảng bá tất cả bit node được thiết lâp bằng 1, làm cho 255 số thập phân nếu tất cả bit được tham chiếu.
  - Vd: Địa chỉ 192.168.10.100/24 có địa chỉ quảng bá là 192.168.10.255
- **Binary Notation(ký hiệu nhị phân)**
  - Do Ipv4 bị giới hạn về số lượng, các mạng IPv4 hiện tại network mask có độ dài thay đổi được sử dụng.
  - Trong subnet mask thay đổi giá trị, chỉ một phần byte được sử dụng để địa chỉ các nút, các phần còn lại được sử dụng cho địa chỉ mạng.
  - Trong subnet mask /, 3 bit đầu sử dụng cho địa chỉ mạng, 5 bit cuối sử dụng cho địa chỉ các nút.
  Network mask: 212.209.113.33/27
  ![image](https://user-images.githubusercontent.com/92305335/139866388-9b6d2c55-a60a-4644-8c9b-d254def8139d.png)
  - Chuyển đổi hệ nhịn phân - thập phân

Giá trị nhị phân| Giá trị thập phân
---|---
00000000 |0
00100000 |32
01000000 |64
01100000 |96
10000000 |128
10100000 |160
11000000 |192
11100000 |224

  - Xét địa chỉ IP 212.209.113.33/27, địa chỉ IP này thuộc về mạng  212.209.113.32/27 và trong địa chỉ quảng bá là 212.2.9.113.63. Với subnet mask /27  30 nút mạng có thể được đánh địa chỉ trên mỗi mạng.
  - Sẽ có 32 địa chỉ để sử dụng, 2 trong số chúng là đia chỉ mạng và địa chỉ quảng bá không thể sử dụng như một địa chỉ IP máy chủ  

**Địa chỉ MAC**
- Địa chỉ MAC dùng để xác định một giao diện mạng duy nhất trong một thiết bị
- Mỗi card mạng sẽ có 12 byte địa chỉ MAC
- Địa chỉ MAC được sử  dụng cho mạng nội bộ(mạng vật lý cuc bộ hoặc mạng WLAN)
- Địa chỉ MAC giúp máy tính tìm được card mạng cụ thể  địa chỉ IP thuộc về
- Vd địa chỉ MAc  00:0c:29:7d:9b:17 với 6 byte đầu chứa ID nhà cung cấp và 6 byte chỉ sự duy nhất của node ID
**Protcol and Port**
- Ở trong note, ta xác định được các dịch vụ đang chạy ví dụ như một web server hoặc FTP server
- Địa chỉ port được sử dụng để xác định dịch vụ.
- VD port 80 dùng cho HTTP (Hypertext Transfer Protocol), port 22 dùng cho SSH, trong giao tiếp mạng người gửi và người nhận sử dụng địa chỉ port
- Vì vậy địa chỉ mạng đích và địa chỉ mạng nguồn liên quan đến giao tiếp mạng.
- Bởi không phải tất cả các dịch vụ được đánh địa chỉ một cách giống nhau nên một Protocal (giao thức) riêng được sử dụng giữa địa chỉ IP và địa chỉ port. VD Transfer Control Protocol (TCP), User Datagram Protocol (UDP), or Internet Control Message Protocol (ICMP).

<a name = '2'></a>
# 2. Quản lý giao diện và địa chỉ mạng
- Địa chỉ mạng có thể được chỉ định theo 2 cách:
  - Fixed IP addresses: hữu ích cho server, luôn luôn cần cho các địa chỉ IP giống nhau.
  - Dynamycally assigned IP addresses: hữu ích cho thiết bị người dùng cuối cùng và cho một phiên bản trong một môi trường  cloud.
- Tên mặc định của card mạng trong linux là eth0, eth1 và  eth2 và hệ thống sẽ dò card mạng bắt đầu từ eth0.
- Trong RHEL 8, tên của card mạng được dựa trên firmware, device topology và device type.
  - Giao diện ethernet bắt đầu bằng *en* , giao diện WLAN bắt đầu bằng *wl* và giao diện WWAN bắt đầu bằng *ww*
  - Tiếp theo là loại adapter. *o* sử dụng cho onboand, *s* sử dụng cho hotplug slot và *p* sử dụng cho PCI location.
  tiếp theo là một số dùng để chỉ định cho index, IP hoặc port
  - Nếu không thể sửa tên thì tên truyền thống sẽ được sử dụng 

- Card mạng có thể được đặt tên dựa vào tên thiết bị BIOS. Để là được điều này, biosdevname package phải được cài đặt.

<a name = '3'></a>
# 3. Xác thực cấu hình mạng

<a name = '31'></a>
## 1.Xác định cấu hình địa chỉ mạng
- Dùng lệnh ip để xác định cấu hình của địa chỉ mạng. 
  - ip addr để cấu hình và giám sát địa chỉ mạng.
  - ip route dùng để cấu hình và giám sát thông tin định tuyến.
  - ip link dùng để cấu hình mà giám sát trạng  thái liên kết mạng.
- Lệnh `ip addr show` để hiển thị cấu hình mạng hiện tại, lệnh `ip a` và `ip a s` có cùng chức năng.

![image](https://user-images.githubusercontent.com/92305335/140005813-e292a8ac-277f-46ee-a273-becde47a2747.png)

  - **Current state**: hiển thị thông tin trạng thái hiện tại là đang hoạt động hay có sẵn.

  - **MAC address configuration**: hiển thị   địa chỉ MAC duy nhất trong mọi card mạng (00:0c:29:cd:53:ee) tương ưng với địa chỉ quảng bá (ff:ff:ff:ff:ff:ff)

  - **IPv4 configuration**: là dòng hiển thị địa chỉ IP hiện sử dụng(và địa chỉ quảng bá tương ứng) cũng như subnet mask được sử dụng.
  -**IPv6 configuration**: là dong hiển thị địa chỉ IPv6  và cấu hình của nó. Địa chỉ IPv6 được mọi giao diện tự động nhận dạng ngay cả khi chưa được cấu hình, nó được sử dụng cho giao tiếp chỉ trong mạng nội bộ.

- Lệnh `ip link show` chỉ hiển thị trạng thái liên kết của giao diện mạng. Thêm tùy chọn -s để hiển thị thống kê số liệu hiện tại.

![image](https://user-images.githubusercontent.com/92305335/140007061-aac63b81-05ae-437e-97b6-bf9d3ae62ca8.png)


<a name = '32'></a>
## 2.Xác thực định tuyến
- Lệnh `ip route show` để xem bộ định tuyến nào được sử dụng, mỗi mạng đều có một bọ định tuyến mặc định được đặt.

![image](https://user-images.githubusercontent.com/92305335/140008304-69114ac1-d4b0-441e-8150-f1a2b0d0ee46.png)

- Dòng `default via 192.168.47.2 dev ens33 proto dhcp metric 100` là phần quan trọng , hiển thị đường định tuyến mặc định đu qua địa chỉ ip 192.168.47.2 và giao diện mạng ens33 cho địa chỉ IP. Nó hiển thị định tuyến mặc định được chỉ thi bởi server DHCP
- Dòng `192.168.47.0/24 dev ens33 proto kernel scope link src 192.168.47.133 metric 100` nhận định nội bộ được kết nối. Ở đây ứng dụng cho mạng 192.168.47.0. Định tuyến này được làm tự động và không cần quản lý.

<a name = '33'></a>
## 3. Xác thực khả dụng của port và server
- Lệnh `netstat` hoặc `ss` để xác định tính khả dụng của port trong server 
- Sử dụng `ss -lt` để hiển thị các TCP port đang sử dụng.

![image](https://user-images.githubusercontent.com/92305335/140010687-311697fd-355c-4f7b-ba56-31e42deb8744.png)

 - Sử dụng lệnh `ip addr add IP-address dev <devicename>`

 - Thêm địa chỉ up IP tạp thời  10.0.0.10/26 `ip addr add 10.0.0.10/26 dev ens33` 

 ![image](https://user-images.githubusercontent.com/92305335/140020326-94724f7c-f9aa-4d7d-808a-89e63bb9d775.png)

- Lệnh `ss -tul` để hiện thị danh sách port ủa UDP và TCP đang listen trong server

![image](https://user-images.githubusercontent.com/92305335/140020504-a94b2219-63f9-4251-88d1-afd744fd2151.png)

<a name = '4'></a>
# 4. Cấu hình mạng với lệnh nmtui và nmcli
- Sử dụng lệnh `systemctl status NetworkManager` để xác đinh trạng thái iệu tại, nó đọc các tập lệnh của cấu hình card mạng ở trong /et/sigconfig/network-scripts và có tên bắt đầu với ifcfg và nối tiếp bởi tên của card mạng 

- Sự khác nhau giữa một thiết bị và một kết nối:
  - Một thiết bị là một card giao diện mạng.
  - Một kết nối là sự cấu hình được sự dụng cho một thiết bị.
- Lệnh nmtui và mncli dùng để quản lý kết nối mạng mà ta muốn chỉ định đến thiết bị.
<a name = '41'></a>
## 1. Quyền yêu cầu thay đổi cấu hình mạng
- Người dùng root có thể sử đổi mạng hiện tại.
- Nếu người dùng bình thường được đăng nhập vào bảng điều kiển nội bộ người dùng đó có thể thay đổi cả cấu hình mạng.
- Lệnh `nmcli gen permissions` để kiểm tra các quyền hiện tại

![image](https://user-images.githubusercontent.com/92305335/140023660-a7218cc9-a9d2-4419-88cc-1498aeefbbb6.png)


<a name = '42'></a>
## 2. Cấu hình mạng với nmcli

- Hiển thị trạng thái kết nối:

![image](image/Screenshot_2.png)

- Lệnh `nmcli con show` để hiểu thị thuộc tính của kết nối 

`nmcli con show ens33` 

![image](image/Screenshot_3.png)

- Lệnh `nmcli dev status` để hiển thị danh sách trạng thái thiết bị 

![image](image/Screenshot_7.png)

- Lệnh `nmcli dev show <devicename>` để xem cài đặt riêng của từng thiết bị 

![image](image/Screenshot_8.png)

VD 
  - Tạo một kết nối mạng mới `nmcli con add con-name eth1 type ethernet ifname ens34 ipv4.method auto`

 ![image](image/Screenshot_58.png)

  - Tạo một kết nối với tên *eth2* để định nghĩa một địa chỉ IP tĩnh và gateway: `nmcli con add con-name eth2 ifname ens33 autoconnect no type ethernet ip4 192.168.247.130/24 gw4 192.168.247.2 ipv4.method manual` 
  
  ![image](image/Screenshot_59.png)
  - Dùng lệnh `vi /etc/sysconfig/network-scripts/ifcfg-eth2` để cấu hình cho mạng eth2

  ![image](image/Screenshot_60.png)

  Trong đó
  DEVICE=eth0	|Tên card mạng
  ---|---
HWADDR=|	Địa chỉ MAC
TYPE=|	Kiểu kết nối
UUID=	|Mã định danh thiết bị (duy nhất)
ONBOOT=|	Kích hoạt card mạng khi khởi động
PREFIX=| sub được máy sử dụng  
NM_CONTROLLED=|	Nếu không sử dụng Network Manager chọn no
BOOTPROTO=|	Sử dụng kết nội động hoặc tĩnh
IPADDR=|Địa chỉ IP
GATEWAY=	|Địa chỉ Gateway
DNS1=	|Địa chỉ DNS

- Lệnh `systemctl restart <service>` để cấu hình có hiệu lực 
- Dùng `nmccli con show` để hiện thị kết nối
- Dùng `nmcli con up eth2` để hoạt động kết nối tĩnh 


- Ngoài ra lệnh `nmcli` còn để dùng thay đổi tham số cấu hình mạng
  -  `nmcli con mod eth2 connection.autoconnect no`: đổi chết độ IP động thành ip tĩnh 
  - `nmcli con mod eth2 ipv4.dns 8.8.8.8` để cài DNS cho IP
  - `nmcli con mod eth2 +ipv4.dns 8.8.4.4` để thêm DNS thứ 2 cho IP
  - `nmcli con mod eth2 ipv4.address 192.168.247.135` để đổi địa chỉ IP thành 192.168.47.135
  - `nmcli con mod eth2 +ipv4.address 192.168.247.136` để thêm  địa chỉ IP thứ 2 là  192.168.47.136
  `nmcli con up eth2` để dùng kết nối eth2

<a name = '43'></a>
## 3. Cấu hình mạng với mntui
 - Lệnh `nmtui` dùng để cấu hình mạng qua giao diện

![image](image/Screenshot_14.png)

- Edit a Connection: tạo một kết nối mới và cấu hình các kết nối hiện có.

![image](image/Screenshot_15.png)

- Activate a Connection: sử dụng để kích hoạt hay vô hiệu kết nối.  

![image](image/Screenshot_16.png)

- Set System Hostname: sử dụng để thiết lập hostname của máy tính.

![image](image/Screenshot_17.png)

<a name = '5'></a>
# 5. Cài Hostname và Name Resolution
- Hostname
  - Dùng lệnh `nmtui` và chọn `Set system hostname`
  - Dùng lệnh `hostnamectl set-hostname`.
  ![image](image/Screenshot_19.png)

  - Sửa nội dung trong file cấu hình  /etc/hostname
- Dùng lệnh `hostnameclt` hay `hostname status` để hiển thị thông tin về  hostname, Linux kernel, virtualization type,...

![image](image/Screenshot_18.png)

- */etc/hosts*  chứa tất cả định nghĩa địa chỉ hostname IP và được áp dụng trước khi hostname trong DNS được sử dụng. Nó được cấu hình như một mặc định trong dòng host trong file *etc/nsswitch.conf*

![image](image/Screenshot_20.png)

- Cấu hình file *etc/hosts* cần đủ 2 cột:
  - Cột 1 chứa thông tin địa chỉ IP của máy chủ riêng
  - Cột 2 chứa hostname riêng
  - Nếu máy chủ có nhiều tên thì cột thứ hai chứa FQDN và cột thứ ba chứa bí danh
- Name Resolution
  - Để máy chủ có thể giao tiếp với các máy chủ khác trên internet, nên sử dụng DNS.
  - Dùng `nmcli` và `nmtui` để thiết lập DNS.
  - Dùng lệnh `nmcli con mod <connection-id> [+]ipv4.dns <ip-of-dns>`
  ![image](image/Screenshot_21.png)
  - Cấu hình DNS trong tệp /etc/sysconfig/network-scripts/ifcfg-nameconnect
![image](image/Screenshot_22.png)
  - Nên thiết lập 2 host DNS để kết nối.
- Nếu sử dụng DHCP thì DNS sẽ được đặt theo DHCP, để thay đổi ta dùng:
  - Sửa file cấu hình của ifcfg với tùy chọn `PEERDNS=no`.
  - DÙng lệnh `nmcli con mod <con-name> ipv4.ignore-auto-dns yes`.
- Lệnh `getent hosts <servername>` để xác định hostname resolution

<a name ='tm'></a>
# Tham khảo

https://phoenixnap.com/kb/configure-centos-network-settings


