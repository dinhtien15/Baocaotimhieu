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
   + Bit Network : dùng để xác định mạng mà thiết bị kết nối vào
   + Bit Host : dùng để xác định thiết bị của mạng đó
   + Broadcast : là địa chỉ dùng đẻ gửi dữ liệu tới toàn bộ các IP trong cùng lớp mạng với nó

3. Cấu hình hosts.allow , hosts.deny : Hai tệp tin này định nghĩa các quy tắc luật truy cập vào hệ thống ở tầng ứng dụng mạng.
   + cú pháp : Deamon: Client [ tùy chọn 1: tùy chọn 2 ]
   + Deamon : Dịch vụ cần áp đặt luật
   + Client : Địa chỉ IP nguồn, host nguồn   
