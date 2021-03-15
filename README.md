# Báo cáo 2
1. Chọn các gói khi cài CentOS
   + DVD ISO : bao gồm tất cả các gói ứng dụng có thể được cài đặt thông qua trình cài đặt
   + Everything ISO : chứa đầy đủ tất cả các gói ứng dụng cho CentOS. Bản này nhiều gói ứng dụng dư thừa, không nên cài
   + NetInstall ISO : là bản mà các gói ứng dụng sẽ được lấy từ mạng và cài đặt 
   + LiveGNOME ISO và LikeKDE ISO : có thể sử dụng thử CentOS thông qua DVD hoặc USB mà không cần cài đặt
   + Minimal ISO : là bản chỉ có những gói ứng dụng cần thiết tối thiểu. Muốn cài thêm ứng dụng phải sử dụng lệnh để cài thủ công. Phù hợp dùng làm server
 
2. Cấu hình căn bản
   + Subnet MASK : Giúp xác định xem trong một địa chỉ IP 32bit, có bao nhiêu bit ở phần Network, bao nhiêu bit ở phần Host
   + Default Gateway : như một cổng thoát hiểm, khi gói tin cần gửi đến địa chỉ không cùng mạng hiện tại, thì gói tin sẽ được gửi đến địa chỉ default gateway, thường là một interface của route nối đến mạng đó. Tại đây route sẽ dùng chức năng định tuyến để chuyển tiếp gói tin đi các hướng khác nhau. default gateway thường là địa chỉ ip có thể sử dụng đầu tiên của mạng đó
   + Frefix Length : là giá trị thường được viết sau một dấu / , giá trị này bằng tổng số bit 1 liên tiếp nhau trong subnet mask
   + Broadcast : là địa chỉ dùng đẻ gửi dữ liệu tới toàn bộ các IP trong cùng lớp mạng với nó
3. Cấu hình hosts.allow , hosts.deny : Hai tệp tin này định nghĩa các quy tắc luật truy cập vào hệ thống ở tầng ứng dụng mạng.
   + cú pháp : Deamon: Client [ tùy chọn 1: tùy chọn 2 ]
   + Deamon : Dịch vụ cần áp đặt luật
   + Client : Địa chỉ IP nguồn, host nguồn   
   + VD  sshd: 192.168.1.1

4. Add bảng định tuyến : static routing là phương thức định tuyến mà người quản trị sẽ nhập tất cả thông tin về đường đi cho router. Nguyên lý hoạt động như sau:
   + người quản trị sẽ cấu hình các đường cố định cho router
   + router sẽ cài đặt đường đi này vào bảng định tuyến
   + gói dữ liệu được định tuyến theo đường cố định
   + Cú pháp : ip route destination_subnet subnetmask{IP_next_hop|output_interface} [AD]
   + destination_subnet : mạng đích đến , subnetmask: subnest mask của mạng đích  , Ip_next_hop : địa chỉ ip của trạm kế tiếp trên đường đi, output_interface:cổng ra trên router , AD: chỉ số AD của route khai báo
   + thêm static route tạm thời : ip route add destinationIP/subnet via route dev [interface]
   + VD : ip route add 172.16.5.0/24 via 10.0.0.101 dev ens33
   + thêm static route vĩnh viễn , tạo 1 tệp trong  /etc/sysconfig/network-scripts/route-[interfaces] , sau đó thêm 1 dòng giống ip route add vd : 172.16.5.0/24 via 10.0.0.101 dev ens33 , khởi động lại mạng dịch vụ(service network restart)

5. Update OS (yum update)
   + kiểm tra bản cập nhật CentOS hiện có : sudo yum check-update
   + dọn dẹp trình quản lý gói : sudo yum clean all
   + khởi động lại máy chủ : reboot
   + cập nhập CentOS : sudo yum update . Hệ thống sẽ cung cấp cho bạn danh sách các gói sẽ tải xuống, dung lượng ổ đĩa cần thiết

6. SELinux : (Security-Enhanced Linux) là một modun bảo mật ở nhân của Linux, cung cấp cơ chế hỗ trợ các chính sách bảo mật kiểm soát truy cập(access control) , bao gồm các điều khiển truy nhập bắt buộc , có 3 mode : Enforcing,Permissive,Disabled
   + Enforcing: chế độ mặc định sẽ cho phép và thực thi chính sách bảo mật SELinux trên hệ thống, từ chối các hành động truy cập và ghi nhật ký
   + Permissive : SELinux được kích hoạt nhưng sẽ không thực thi chính sách bảo mật, chỉ cảnh báo và ghi lại các hành động
   + Disable : SELinux bị vô hiệu hóa hoặc bị tắt đi

7. Permitsion của file , thư mục
   + lệnh chmod : thay đổi quyền hạn đối với file, cú pháp #chmod[option][MODE] <file or thư mục> , vd #chmod 755 text.txt
   + lệnh chown : thay đổi quyền sở hữu file , cú pháp #chown [option] user:group <file or thư mục> , vd #chown apache:apache web_directory , vd #gán user1 là chủ sở hữu thư mục /data/userlist: #chown user1 /data/userlist
   + lệnh chgrp : thay đổi nhóm sở hữu , cú pháp #chgrp [option] <group> <file or thư mục>, vd #chgrp -c user text.txt
   + quyền r : cho phép mở file và đọc
   + quyền w : cho phép ghi vào file hoặc xóa nội dung file, không cho phép xóa hoặc rename
   + quyền x : cho phép file được coi như một ctrinh có thể thực thi được
   + file ext3 : là file hệ thống nâng cấp của ext2, ext3 đưa vào thêm chức năng mới vô cùng quan trọng là journaling file system giúp thao tác dữ liệu an toàn hơn
   + file ext4 : là file mở rộng nâng cấp từ ext3 với khả năng tương thích ngược , là tổng hơp của các file ext trước cộng lại,chống phân mảnh dữ liệu.

8. Tạo user,group, cấu hình sudo cho user mới
   + thêm user mới : adduser tientapta
   + thêm mk : #passwd ....
   + cấp quyền sudo cho user vừa tạo bằng cách thêm vào nhóm wheel(các thành viên trong nhóm wheel mặc định sẽ có đặc quyền sudo) : #usermod -aG wheel tientapta
   + kiểm tra lại người dùng với quyền sudo : #cat /etc/group | grep tientapta

9.Đổi port ssh, cấu hình ssh giới hạn user truy cập
   + vô hiệu hóa đăng nhập từ xa với user root : ->truy cập file sshd_config, trong file này chỉnh PermitRootLogin no, sau đó khởi động lại ssh : #systemctl restart sshd
   + đổi port ssh truy cập /etc/ssh/sshd_config , có phần Port rồi chuyển sang port mà chúng ta cần sau đó lưu file lại
   + Cho phép user hoặc group user được phép đăng nhập ssh , thêm mới vào file /etc/ssh/sshd_config, # AllowUsers user1 user2 , # AllowGroups Group1
   + Không cho phép user hoặc group user được phép đăng nhập ssh, # DenyUsers user1 user2, # DenyGroups Group1
  
10. Keepass : là một phần mềm mã nguồn mở miễn phí giúp lưu trữ tất cả mật khẩu,thông tin cá nhân. Chương trình này lưu trữ password của bạn trong một file csdl được mã hóa ở mức cao

11. DenyHosts : một công cụ bảo mật ngăn chặn xâm nhập dựa trên nhật ký cho các máy chủ SSH được viêt bằn Python. DenyHosts được thiết kế để ngăn chặn các cuộc tấn công brute-force vào các máy chủ ssh bằng cách giám sát các nỗ lực đăng nhập không hợp lệ trong nhật ký xác thực và chặn các địa chỉ IP gốc bằng cách sử dụng /etc/hosts.deny. Cách cài đặt
   + sudo apt-get install denyhosts
   + truy cập tệp cấu hình /etc/denyhosts.conf , có rất nhiều luật mình có thể đặt như BLOCK_SERVICE = sshd , hoặc giới hạn ngưỡng từ chối đăng nhập DENY_THRESHOLD_ROOT = 1
   + khởi động lại denyhosts : # sudo systemctl restart denyhosts.service
   + bật denyhosts vào thời gian khởi động : # sudo systemctl enable denyhosts.service
   + xem tệp nhật ký /var/log/allowhosts để tìm lỗi : # sudo grep 'something' /var/log/denyhosts
   + Xem danh sách các hosts bị block : # sudo cat /etc/hosts.deny
   + bật denyhosts : sudo systemctl start denyhosts.service
   + tắt denyhosts : sudo systemctl stop denyhosts.service
   
13. TCP Wapper : là một phương pháp chặn truy cập các dịch vụ trên máy chủ Linux của bạn với sự trợ giúp của 2 tệp cấu hình /etc/hosts.allow và /etc/hosts.deny
   + hosts.allow sẽ được ưu tiên hơn hosts.deny . Nesey xảy ra trường hợp cả 2 file này đều allow và deny cùng 1 IP, thì IP này sẽ vẫn được allow
   + bất kỳ thay đổi nào trong 2 file đều có hiệu lực ngay lập tức
   
