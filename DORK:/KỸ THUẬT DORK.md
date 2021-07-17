Mình để ý thấy có nhiều bạn đang bị lu mờ giữa 2 khái niệm Pentest và Hacking. Thực sự thì cũng sẽ khó có thể phân biệt rõ ràng nhưng "Hacking" là cụm từ chỉ hành động khi bạn tìm thấy lổ hổng (cả về lổ hổng logic và lổ hổng đến từ tech) và khai thác được lổ hổng đó. Còn Pentest theo mình thì chỉ là kiểm tra đánh giá tính bảo mật của một hệ thống hoặc một server nào đó thôi.. <(")

## Goole Hacking Database (GHDB) là gì?

OK! Bắt đầu với chủ đề mà mình đề cập tới sau đây. Có nhiều bạn hỏi mình: **"Làm sao để có thể nhanh chóng tìm được lỗi từ ứng dụng web?"**. Câu trả lời của mình là:**"Hãy bắt đầu với Google Hacking."**
Google Hacking là một thuật ngữ mà gói gọn một loạt các kĩ thuật cho phép truy vấn trên công cụ tìm kiếm Google.com, đôi khi được dùng để xác định các lổ hổng trong các ứng dụng web cụ thể.(Cụ thể như thế nào thì mình sẽ cố gắng giải thích tiếp trong giới hạn kiến thức mà mình biết). 

Bên cạnh việc truy vấn từ google có thể tiết lộ các lỗ hổng trong các ứng dụng web, Google Hacking cho phép bạn tìm các dữ liệu nhạy cảm, có ích cho giai đoạn Reconnaissance để attack ứng dụng, chẳng hạn như email liên kết với một trang web nào đó, cơ sở dữ liệu hoặc các file khác với tên người dùng và mật khẩu, các thư mục không được bảo vệ với các tập tin nhạy cảm, URL để đăng nhập cổng thông tin, các loại khác nhau của các bản ghi hệ thống như tường lửa và truy cập các bản ghi....etc.

## Truy vấn nâng cao cho Search Engine Google!

Việc truy vấn cao cấp cho phép bạn có được kết quả tìm kiếm cụ thể hơn từ các truy vấn của bạn, hầu hết đều là các kết quả có liên quan và hữu ích nhât.(*Mình phải công nhận Google đã xây dựng nên một bộ công cụ tìm kiếm không chỉ giúp ích cho người dùng cuối 😧 *).
Ví dụ bạn có thể sử dụng các truy vấn để có được các tập tin mà bạn cần chỉ xuất phát từ một hoặc một vài trang web nào đó. Điều này có thể được thể hiện bằng cách truy vấn trên Google cho một tên miền sử dụng `site:tld`.
Ví dụ bạn có thể sử dụng: `site:vn filetype: pdf`

Dưới đây là một số operator mình hay sử dụng, hôm qua trong buổi stream mình cũng đã sử dụng qua một số loại

| **OPERATOR**  |  **EXPLAIN** |  **EXAMPLE** |
| :------------: | :------------: | :------------: |
|intitle: | Tìm kiếm trong phần title của trang web	  | intitle:index.of inurl:hits  |
|inurl:   | Tìm kiếm với url đường dẫn trang web   | inurl:.ssh intitle:index.of authorized_keys|
|intext: | Tìm kiếm với phần nội dụng của web(Phần nội dung thường được truy cập bởi người dùng)	  | intext:”server-status”  |
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

![image](https://user-images.githubusercontent.com/53977417/121766020-50158100-cb79-11eb-859c-22615bf93412.png)

![image](https://user-images.githubusercontent.com/53977417/121766097-d7fb8b00-cb79-11eb-8706-43b41ce60275.png)

Điều này sẽ tìm kiếm cơ sở dữ liệu đã lưu vào các trang web có URL chứa các từ sao lưu và wp-content. Wp-content là thư mục mà người sử dụng và một số plugin tải lên tập tin của họ trong các CMS WordPress phổ biến mà nhiều trang web đang được xây dựng, và backup có khả năng có thể lọc kết quả cho người dùng.
Có rất nhiều các tập tin được sử dụng bởi các loại khác nhau của phần mềm có chứa danh sách tên người dùng và mật khẩu.

### Xác định thông tin phiên bản!

Truy vấn như intitle:index.of server.at có thể xác định danh sách thư mục với một số thông tin máy chủ được thể hiện trong danh sách này bởi mặc định trong các máy chủ web như Apache. Ví dụ, một tìm kiếm cho intitle:index.of server.at site:somewebsite.edu tiết lộ các phần mềm đặc biệt server (Apache), phiên bản của nó và hệ điều hành của máy nó là như đã thấy trong hình dưới đây.

![image](https://user-images.githubusercontent.com/53977417/121766197-94ede780-cb7a-11eb-84b2-599096870249.png)

Qua đó, ta có thể thấy rằng có thể tìm kiếm các trang web đang sử dụng các phần mềm, ứng dụng bị lỗi. Công việc này tưởng chừng như vô nghĩa và thường bị các newbie bỏ qua. Sau đó bạn sẽ thấy rằng một phiên bản PHP 5.2 và phiên bản PHP 5.6 nó lỗi tè le như thế nào. 🔢 
