# Automated Analysis Of Malicious Microsoft Office Documents

[Reference Paper Link](https://www.sciencedirect.com/science/article/pii/S0167404821004053?)


    Keywords:
    Malware
    Office documents
    Macro malware
    Powershell
    LOLBAS

- Abstract:

`Cho đến nay, Microsoft Office có thể là bộ ứng dụng được sử dụng rộng rãi nhất để xử lý tài liệu, bảng tính và bản trình bày. Do tính phổ biến của nó, nó liên tục được sử dụng để thực hiện các chiến dịch độc hại.` Các tác nhân đe dọa, khai thác các tính năng động của nền tảng, sử dụng nó để khởi động các cuộc tấn công và thâm nhập hàng triệu máy chủ trong chiến dịch của họ.
<br><br>
Công việc này khám phá bối cảnh hiện đại của các tài liệu Microsoft Office độc ​​hại, chỉ ra các phương tiện mà các tác giả phần mềm độc hại sử dụng. Chúng tôi tận dụng sự phân loại của các công cụ được sử dụng để xử lý các tài liệu Microsoft Office và khám phá hoạt động của các tác nhân độc hại. Hơn nữa, chúng tôi đã tạo và chia sẻ công khai một `tập dữ liệu được chế tạo đặc biệt, dựa trên việc kết hợp các tài liệu lành tính và độc hại có chứa nhiều tính năng động như macro VBA và DDE.` Điều sau là rất quan trọng cho một phân tích công bằng và thực tế, một vấn đề mở trong tình trạng nghệ thuật hiện nay. Điều này cho phép chúng tôi đưa ra kết luận an toàn về các tính năng và hành vi độc hại. Chính xác hơn, chúng tôi trích xuất các tính năng cần thiết bằng quy trình phân tích tự động để phân loại hiệu quả và chính xác tài liệu là lành tính hay độc hại bằng cách sử dụng máy học với điểm F1 trên 0,98, vượt trội so với các thuật toán phát hiện hiện đại nhất.

## 1. Introduction:

`Microsoft Office cho đến nay vẫn là bộ ứng dụng văn phòng được sử dụng rộng rãi nhất.` Các tài liệu được tạo ra từ bộ phần mềm không có nghĩa là tĩnh và chứa nhiều yếu tố động để làm cho chúng trở nên dễ chịu hơn về mặt thẩm mỹ, cung cấp các chức năng và tương tác nâng cao. Bản chất động của các phần tử được tăng cường thêm khi sử dụng ngôn ngữ lập trình `VBA (Visual Basic for Applications).` Tuy nhiên, nhiều lợi ích mà sự hỗ trợ từ một ngôn ngữ như vậy có thể mang lại nhưng phải trả một cái giá đắt. Lý do là kẻ thù có thể bọc giáp các tài liệu để tiến hành một cuộc tấn công. Trên thực tế, các tài liệu văn phòng độc hại được các thực thể độc hại sử dụng rộng rãi để phát tán phần mềm độc hại trên toàn thế giới, thường là thông qua email. Do được chuyển lại bởi nhiều nguồn khác nhau (Avira, 2020; ESET, 2020), tài liệu MS Office là định dạng tệp được phần mềm độc hại cho Windows sử dụng rộng rãi thứ hai và liên tục được sử dụng trong các chiến dịch malspam (Crowdstrike, 2020; Patsakis và Chrysanthou, 2020) .
<br><br>
`Lý do chính mà các tệp này được sử dụng thường xuyên trong các chiến dịch như vậy là chúng được người dùng trao đổi liên tục. Do đó, người dùng có nhiều khả năng sẽ tải xuống và mở tệp MS Office mà họ nhận được, ngay cả từ một người gửi không xác định,` ví dụ: tệp thực thi hoặc định dạng tệp “lạ”. Về vấn đề này, một tệp MS Office được kẻ thù sử dụng để đặt chân vào máy của nạn nhân và sau đó tiến hành lây nhiễm thực sự cho máy chủ. `Trong khi AV có nhiều biện pháp kiểm tra cụ thể để ngăn chặn sự lây nhiễm từ các tệp như vậy, ngoài một số biện pháp kiểm soát được chế tạo đặc biệt từ MS cho phép người dùng cấp quyền thực thi một cách có chọn lọc, người dùng vẫn trở thành nạn nhân của các cuộc tấn công này.` Đáng chú ý, một trong những phần mềm độc hại khét tiếng nhất trên toàn thế giới gần đây đã bị gỡ xuống Malwarebytes, Emotet, đang sử dụng các tài liệu MS Office bọc thép để lây nhiễm.

### 1.1. Motivation and contribution:

Mục tiêu của công việc này là thực hiện phân tích kỹ lưỡng các tài liệu MS Office độc ​​hại cho đến nay và thiết lập hiểu biết cơ bản về hoạt động mô-đun của chúng thông qua một cách tiếp cận tự động. Để đạt được mục tiêu này, chúng tôi đã thiết lập một `quy trình tự động bao gồm một tập hợp các bước phân tích tài liệu cả tĩnh và động, đồng thời trích xuất một tập hợp các tính năng có thể được sử dụng để tạo điều kiện phân loại tài liệu từ lành tính đến độc hại.`
<br><br>
Sự đóng góp của công việc này là rất nhiều. Phần lớn công việc trong các tài liệu MS Office độc ​​hại đang tập trung vào các tính năng có thể được sử dụng để phát hiện các tài liệu độc hại, nhưng không tập trung vào lý do thực tế tại sao chúng tồn tại. Trong bối cảnh này, chúng tôi thực sự tiết lộ những gì một tài liệu độc hại làm. Trái ngược với việc chỉ đơn giản nói rằng, ví dụ: chuỗi hex được sử dụng, thông qua thử nghiệm mở rộng, chúng tôi cho thấy rằng mặc dù có khả năng tiềm ẩn, nhưng các tài liệu MS Office độc ​​hại này thực sự là các ống nhỏ giọt; họ tải xuống và thực thi một tải trọng độc hại. Trong bối cảnh này, bài báo của chúng tôi là bài báo đầu tiên định lượng vấn đề thể hiện `những phương tiện nào để thực hiện tải trọng bị giảm.` Theo hiểu biết tốt nhất của chúng tôi, đây là bài báo đầu tiên trong tài liệu học thuật `sử dụng giải mã để chỉ ra điều này trong khi hầu hết các tác giả chỉ đơn giản coi việc làm nhiễu loạn là một dấu hiệu của sự độc hại. Điều thứ hai có nghĩa là họ phát hiện ra triệu chứng nhưng không phát hiện ra nguyên nhân của nó. Ngoài ra, ngoài việc chỉ báo cáo LOLBAS / LOLBIN đã sử dụng, chúng tôi cho thấy sự đa dạng của các lựa chọn này cho thấy rằng một số giải pháp EDR và ​​EPP, mặc dù biết vectơ tấn công này không chặn chúng một cách hiệu quả.` Điều sau biện minh cho tác động cao của các chiến dịch phần mềm độc hại sử dụng cách tiếp cận này.
<br><br>
Một đóng góp rất quan trọng cũng là tập dữ liệu mà chúng tôi đang sử dụng. Như chúng ta sẽ thảo luận sau trong bản thảo, các tập dữ liệu thiên vị, chẳng hạn như không bao gồm các tài liệu MS Office với mã VBA có thể dễ dàng thể hiện kết quả xuất sắc, nhưng trên thực tế, hoạt động khá kém. Ngược lại, tập dữ liệu của chúng tôi được tạo ra để ngăn chặn những thành kiến như vậy. Cái sau được sử dụng để xác định các tính năng không được sử dụng trong tài liệu, ví dụ:` VBA stomping, DDE, v.v. cho phép chúng tôi phát hiện các mẫu phần mềm độc hại khai thác, ví dụ: lỗ hổng MS Office mới`, không xác định tại thời điểm bài viết được gửi ban đầu . Phần sau minh họa rõ ràng hiệu quả và tiềm năng của phương pháp được đề xuất. Cuối cùng, các tính năng đã chọn và cách tiếp cận máy học rõ ràng vượt trội hơn so với công việc hiện có trong lĩnh vực này. Do các đặc điểm của tập dữ liệu này, để đảm bảo tính uy tín của kết quả của chúng tôi và để thúc đẩy nghiên cứu trong lĩnh vực này, tập dữ liệu được cung cấp trong Zenodo (Koutsokostas et al., 2021).
<br><br>
Trong phần tiếp theo, trước tiên chúng tôi cung cấp tổng quan về công việc liên quan đến phần mềm độc hại và tài liệu văn phòng. Cuối cùng, chúng tôi phân tích cấu trúc của chúng, các phương pháp được sử dụng để bọc giáp chúng, một số biện pháp đối phó và phương pháp phát hiện cũng như một số công cụ mã nguồn mở được sử dụng để xử lý các tệp MS Office. Sau đó, chúng tôi thảo luận về phương pháp của chúng tôi về thu thập, xử lý và phân tích dữ liệu. Sau đó, trong Phần 3, chúng tôi cung cấp tổng quan về tập dữ liệu của chúng tôi và một số phân tích khám phá về nội dung của nó. Phần 5 phân tích các phát hiện của chúng tôi và Phần 6 thảo luận về các phương pháp đã được xác định từ mỗi phần trong phương pháp của chúng tôi, cũng như hiệu quả và nhược điểm của chúng. Cuối cùng, bản thảo kết luận tóm tắt những phát hiện và đóng góp của chúng tôi.

## 2. Related work

Trong phần này, chúng tôi cung cấp cho người đọc những thông tin cơ bản cần thiết và tổng quan về công việc liên quan sẽ được sử dụng trong công việc của chúng tôi. Vì vậy, trước tiên chúng ta thảo luận về cấu trúc của các tài liệu được hỗ trợ bởi MS Office. Sau đó, chúng tôi trình bày các phương pháp cơ bản được đối thủ sử dụng để tạo lớp giáp cho tệp MS Office và các phương pháp được sử dụng để phát hiện các tài liệu đó. Cuối cùng, chúng tôi trình bày các công cụ nguồn mở nổi tiếng nhất được sử dụng để tạo các tài liệu MS Office độc hại hoặc để làm phong phú thêm khả năng của chúng.

### 2.1. Files supported by MS Office and their structure:

`MS Office hỗ trợ một số định dạng tài liệu; tuy nhiên, cốt lõi của hầu hết các tài liệu là XML.` Các định dạng này đã được giới thiệu khoảng hai thập kỷ trước trong Office XP để hỗ trợ định dạng dựa trên XML cho Excel và tiếp tục vào năm 2002 với một định dạng XML khác cho Word. Các định dạng này được tích hợp và trở thành định dạng mặc định cho MS Office 2003. Tuy nhiên, kể từ `MS Office 2007, MS đã áp dụng định dạng Office Open XML, còn được gọi là định dạng OpenXML hoặc OOXML, cho phép khả năng tương tác với các bộ và phần mềm xử lý tương tự khác. Định dạng Office Open XML dựa trên XML và đã được ECMA International áp dụng với tên gọi ECMA-376 (Ecma International, 2006) và trở thành tiêu chuẩn quốc tế (ISO / IEC 29500)` (International Organization for Standardization, 2016). Rõ ràng, về khả năng tương thích và khả năng tương tác, MS Office hỗ trợ tất cả các định dạng trước đó.
<br><br>
Các tệp theo định dạng OOXML là các gói chứa một số tệp XML cụ thể cùng với các tệp và tập lệnh đa phương tiện, được nén ở dạng tệp ZIP. Phần tử quan trọng của gói là tệp .xml [Content_Types] được lưu trữ trong thư mục gốc của gói. Tệp này đóng vai trò là chỉ mục của gói và liệt kê tất cả các kiểu nội dung của các phần mà gói chứa. Hai thư mục chính là _rels, lưu trữ các mối quan hệ giữa các phần khác và tài nguyên bên ngoài gói và docProps chứa các thuộc tính cốt lõi của tệp OOXML. Sau đó, tùy thuộc vào tệp, người ta có thể tìm thấy một thư mục word hoặc xl chứa nội dung của tệp. Trong các thư mục này, người ta thường có thể tìm thấy tệp vbaProject.bin; tài liệu tổng hợp OLE (Microsoft, 2020a) ở định dạng nhị phân, chứa mã VBA cho các macro mà OOXML có thể có. Cấu trúc điển hình của tài liệu OOXML và tệp bảng tính được minh họa ở bên trái và bên phải của Hình 1, tương ứng

![image](https://user-images.githubusercontent.com/62002485/164983031-17725416-a8f4-46e4-ba2c-876846017f8c.png)
<br><br>
Ngoài các định dạng trên, MS Office hỗ trợ các định dạng khác, trong đó quan trọng nhất từ góc độ bảo mật là Định dạng nhị phân tệp kết hợp (CFBF), là các tệp lưu trữ có cấu trúc (Microsoft, 2018b), tệp XLSB (Microsoft, 2021) cho MS Excel, có định dạng nhị phân và nhanh hơn đáng kể so với các tệp XLS / XLSX truyền thống.

### 2.2. Malicious MS Office files and their detection:

Không phải quá nhiều định dạng tệp khác nhau mà MS Office hỗ trợ đã tạo ra các vấn đề, mà thực tế là các định dạng này được thiết kế để hỗ trợ các tài liệu động. Tính năng động này được kích hoạt thông qua các thành phần và mô-đun khác nhau sử dụng nhiều phần lập trình. `Phần rõ ràng nhất là sự hỗ trợ cho VBA, cho phép ai đó viết mã tùy ý và thực thi nó bất cứ khi nào thấy cần thiết, thậm chí tự động khi tệp được mở hoặc đóng. Điều quan trọng là mã VBA không bị cô lập trong ngữ cảnh tài liệu MS Office, nhưng nó có thể tương tác với hệ thống tệp, trao đổi dữ liệu qua Internet và thực hiện các lệnh shell. Rõ ràng là những điều trên khiến người dùng gặp phải những rủi ro nghiêm trọng và đã được sử dụng rộng rãi trong phạm vi tấn công mạng trong nhiều năm. Ngoài VBA, người ta có thể thực hiện các tác vụ tương tự bằng cách sử dụng macro XLM (Microsoft, 2020b) và giao thức Trao đổi dữ liệu động (DDE)` (Microsoft, 2018a) hoặc sử dụng tài liệu XML thuần túy (Mendrez, 2015).
<br><br>
Một cuộc tấn công điển hình bằng cách sử dụng tài liệu MS Office được minh họa trong Hình 2. `Khi người dùng mở một tệp độc hại với MS Of fice, kẻ thù sẽ sử dụng trình kích hoạt để khởi chạy một tập lệnh VBA (ví dụ: orkbook_Open (), AutoOpen () và chức năng AutoClose ()) hoặc tự động đánh giá các giá trị động của tài liệu được liên kết với DDE (sử dụng ví dụ: Trình chỉnh sửa phương trình hoặc các phương trình ô) hoặc macro XLM được liên kết với ô. Mặc dù mã có thể thực hiện một số tác vụ, trong hầu hết các chiến dịch, ví dụ: Emotet (Patsakis và Chrysanthou, 2020), mã sẽ tải xuống một tải trọng từ Internet hoặc trích xuất nó từ chính tài liệu.` Tuy nhiên, điều này dẫn đến một vấn đề mới nhất cho đối thủ

![image](https://user-images.githubusercontent.com/62002485/164983314-e4c49732-3460-4c44-9166-5248bf684db2.png)


Các phiên bản Windows dưới dạng tệp đã tải xuống sẽ không được ký bởi cơ quan đáng tin cậy. Do đó, Kiểm soát tài khoản người dùng (UAC) của Windows sẽ yêu cầu sự đồng ý rõ ràng của người dùng để cho phép thực thi tệp. Vì người dùng rất có thể sẽ từ chối yêu cầu đó, các tài liệu độc hại sẽ tuân theo một cách tiếp cận khác. Thay vì thực hiện trực tiếp tải trọng độc hại, chúng sử dụng "proxy" được hệ điều hành tin cậy, ví dụ: PowerShell, Explorer. Có một số mã nhị phân và tập lệnh được cài đặt sẵn trong Windows hoặc được tải xuống bởi MS và được hệ điều hành ký hoặc đưa vào danh sách trắng, đồng thời cho phép thực hiện các chức năng bổ sung và có thể khai thác. Do chữ ký của họ, họ bỏ qua UAC của Windows, cho phép trong số những người khác thực thi mã tùy ý, biên dịch mã, cũng như tải xuống / tải lên tệp, xử lý kết xuất và thu thập thông tin đăng nhập mà không yêu cầu bất kỳ tương tác nào của người dùng. Các tệp nhị phân và tập lệnh này được gọi là Living Off The Land Binaries và Scripts (và cả Thư viện) hoặc LOLBAS (Campbell và cộng sự, 2020) và được sử dụng rộng rãi bởi các nhóm đỏ và phần mềm độc hại. Do đó, các tài liệu độc hại sử dụng LOLBAS để thực thi tải trọng độc hại và lây nhiễm sang máy chủ lưu trữ một cách liền mạch.
