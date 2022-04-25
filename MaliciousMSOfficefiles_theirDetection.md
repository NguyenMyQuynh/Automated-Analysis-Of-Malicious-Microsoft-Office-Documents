# Malicious MS Office files and their detection

Tài liệu lành tính và độc hại có chứa nhiều tính năng động như macro VBA, tài liệu MS Office với mã VBA(ngôn ngữ lập trình VBA-Visual Basic for Applications).
Ngoài VBA, người ta có thể thực hiện các tác vụ tương tự bằng cách sử dụng macro XLM (Microsoft, 2020b) và giao thức Trao đổi dữ liệu động (DDE)

Khi người dùng mở một tệp độc hại với MS Office, kẻ thù sẽ sử dụng trình kích hoạt để khởi chạy một tập lệnh VBA 
(ví dụ: orkbook_Open (), AutoOpen () và chức năng AutoClose ()) hoặc tự động đánh giá các giá trị động của tài liệu được liên kết với DDE
Mặc dù mã có thể thực hiện một số tác vụ, trong hầu hết các chiến dịch, mã sẽ tải xuống một tải trọng từ Internet hoặc trích xuất nó từ chính tài liệu.

Dự án Living off the Land Binaries and Scripts (LOLBAS) nhằm mục đích ghi lại tất cả các tập lệnh và mã nhị phân đã được Microsoft ký kết bao gồm chức năng cho các nhóm APT trong các cuộc tấn công của Living off the Land. Cho đến nay, có 135 công cụ hệ thống trong danh sách này dễ bị lạm dụng, mỗi công cụ hỗ trợ một mục tiêu khác nhau. Đó có thể là việc tạo tài khoản người dùng mới, nén và lọc dữ liệu, thu thập thông tin hệ thống, khởi chạy các quy trình trên một điểm đến mục tiêu hoặc thậm chí là vô hiệu hóa các dịch vụ bảo mật.

![image](https://user-images.githubusercontent.com/62002485/165015428-1153c90a-aef5-43ea-9fe0-13a5c1a0ec58.png)
