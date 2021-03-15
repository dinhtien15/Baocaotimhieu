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
   + thêm static route vĩnh viễn , tạo 1 tệp trong  /etc/sysconfig/network-scripts/route-[interfaces] , sau đó thêm 1 dòng giống ip route add , khởi động lại mạng dịch vụ(service network restart)

5. TCP Wapper : là một phương pháp chặn truy cập các dịch vụ trên máy chủ Linux của bạn thông qua hạn chế IP
   + hosts.allow sẽ được ưu tiên hơn hosts.deny . Nesey xảy ra trường hợp cả 2 file này đều allow và deny cùng 1 IP, thì IP này sẽ vẫn được allow
   + bất kỳ thay đổi nào trong 2 file đều có hiệu lực ngay lập tức

6. Permitsion của file , thư mục
   + quyền r : cho phép mở file và đọc
   + quyền w : cho phép ghi vào file hoặc xóa nội dung file, không cho phép xóa hoặc rename
   + quyền x : cho phép file được coi như một ctrinh có thể thực thi được

7. Keepass : là một phần mềm mã nguồn mở miễn phí giúp lưu trữ tất cả mật khẩu,thông tin cá nhân. Chương trình này lưu trữ password của bạn trong một file csdl được mã hóa ở mức cao
