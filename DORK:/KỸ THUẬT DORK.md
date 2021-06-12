Mình để ý thấy có nhiều bạn đang bị lu mờ giữa 2 khái niệm Pentest và Hacking. Thực sự thì cũng sẽ khó có thể phân biệt rõ ràng nhưng "Hacking" là cụm từ chỉ hành động khi bạn tìm thấy lổ hổng (cả về lổ hổng logic và lổ hổng đến từ tech) và khai thác được lổ hổng đó. Còn Pentest theo mình thì chỉ là kiểm tra đánh giá tính bảo mật của một hệ thống hoặc một server nào đó thôi.. <(")

## Goole Hacking Database (GHDB) là gì?

OK! Bắt đầu với chủ đề mà mình đề cập tới sau đây. Có nhiều bạn hỏi mình: **"Làm sao để có thể nhanh chóng tìm được lỗi từ ứng dụng web?"**. Câu trả lời của mình là:**"Hãy bắt đầu với Google Hacking."**
Google Hacking là một thuật ngữ mà gói gọn một loạt các kĩ thuật cho phép truy vấn trên công cụ tìm kiếm Google.com, đôi khi được dùng để xác định các lổ hổng trong các ứng dụng web cụ thể.(Cụ thể như thế nào thì mình sẽ cố gắng giải thích tiếp trong giới hạn kiến thức mà mình biết). 

Bên cạnh việc truy vấn từ google có thể tiết lộ các lỗ hổng trong các ứng dụng web, Google Hacking cho phép bạn tìm các dữ liệu nhạy cảm, có ích cho giai đoạn Reconnaissance để attack ứng dụng, chẳng hạn như email liên kết với một trang web nào đó, cơ sở dữ liệu hoặc các file khác với tên người dùng và mật khẩu, các thư mục không được bảo vệ với các tập tin nhạy cảm, URL để đăng nhập cổng thông tin, các loại khác nhau của các bản ghi hệ thống như tường lửa và truy cập các bản ghi....etc.

## Truy vấn nâng cao cho Search Engine Google!

Việc truy vấn cao cấp cho phép bạn có được kết quả tìm kiếm cụ thể hơn từ các truy vấn của bạn, hầu hết đều là các kết quả có liên quan và hữu ích nhât.(*Mình phải công nhận Google đã xây dựng nên một bộ công cụ tìm kiếm không chỉ giúp ích cho người dùng cuối :D*).
Ví dụ bạn có thể sử dụng các truy vấn để có được các tập tin mà bạn cần chỉ xuất phát từ một hoặc một vài trang web nào đó. Điều này có thể được thể hiện bằng cách truy vấn trên Google cho một tên miền sử dụng `site:tld`.
Ví dụ bạn có thể sử dụng: `site:vn filetype: pdf`

Dưới đây là một số operator mình hay sử dụng, hôm qua trong buổi stream mình cũng đã sử dụng qua một số loại

| **OPERATOR**  |  **EXPLAIN** |  **EXAMPLE** |
| :------------: | :------------: | :------------: |
|intitle: | Tìm kiếm trong phần title của trang web	  | intitle:index.of inurl:hits  |
|inurl:   | Tìm kiếm với url đường dẫn trang web   | inurl:.ssh intitle:index.of authorized_keys|
|intext: | Tìm kiếm với phần nội dụng của web(Phần nội dung thường được truy cập bởi người dùng)	  | inurl:”server-status”  |
|allintext:/allinurl:/allintitle:	 | Cái này hơi phức tạp. Đại loại là nó làm việc tương tự với những cái phía trên	  | allintitle:Welcome to Windows XP Server Internet Services  |
|filetype:| Giới hạn các loại tập tin mong muốn (*:D. Cái này các bạn vừa thấy ở trên*)	  | filetype: xls intext:email intext: password|
| site:  | Giới hạn kết quả các trang web đã cho.	  | intitle:”index.of” site:mit.edu|
| Info:| Cái này thì nó show toàn bộ các thông tin liên quan đến các webpage liên kết, thậm chí là cho phép show được cả cache các trang được lưu trữ	  |  infor:apple.com|
|  cache: |  Lấy tất cả các cache mà Google có cho các trang nhât định	 | cache:sitepoint.com/javascripts/|
| –	  | Bao gồm các điều kiện khác	  | inurl:citrix inurl:login.asp -site:citrix.com|
| “search-term”	  | Ý là bao quanh cụm từ bằng dấu "", tìm kiếm chính xác.	  | inurl:”server-status” intext:”Apache Server Status”|
|  * | Tương tự như dùng trong terminal nhé. Kí tự đại diện cho các từ chưa biết.	  | a * saved is a * earned|
|   +|  Thường để cố định các kết quả theo cụm từ mình muốn, Bởi Google thường có xu hướng bỏ qua các từ quá thông dụng trong câu truy vấn	  | “Machine gun” +uzi|
|   .|  kí tự đại diện cho bất kì kí tự nào tại vị trí đó trong cụm từ tìm kiếm	 |  inurl:.ssh intitle:index.of authorized_keys|

## Google Hacking Database

Google Hacking Database chia thành nhiều loại khác nhau như: thông tin các file bị tổn thương, các file chứa mật khẩu, thông tin về máy chủ và phần mềm trên đó, tìm kiếm các thiết bị trực tuyến...etc. Một Dork chỉ là một truy vấn Google đã tìm ra kết quả hữu ích như khai thác dữ liệu nhạy cảm. Khi duyệt qua các kết quả, bạn nên tham khảo đến thời gian update hoặc thời gian được lữu trữ, Google hỗ trợ điều đó rất tốt từ các kết quả mà nó mang lại cho bạn. Một vài kết quả từ lâu sẽ bao gồm là các thông tin phiên bản ứng dụng gặp lỗi, lỗi ứng dụng code,...everything.
Kiểm tra thâm nhập cơ bản thông qua Google Hacking
Có nhiều cách để tìm kiếm username và password người dùng thông qua các truy vấn của Google. Ví dụ bạn có thể tìm kiếm các file sql có chứa các dữ liệu của các trang web.

### Kiểm tra thâm nhập cơ bản thông qua Google Hacking

Có nhiều cách để tìm kiếm username và password người dùng thông qua các truy vấn của Google. Ví dụ bạn có thể tìm kiếm các file sql có chứa các dữ liệu của các trang web.


