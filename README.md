# Tool-report
Dự án này là một bộ các script Python được thiết kế để tự động hóa các tác vụ liên quan đến việc kiểm tra, thu thập bằng chứng và gửi báo cáo về các trang web có dấu hiệu vi phạm hoặc độc hại.
---
### ✨ Các Script trong Dự Án
**sheet.py**: Tải dữ liệu từ một Google Sheet công khai (được cấu hình sẵn), lọc ra các domain "còn sống" và lưu chúng vào file urls.txt để xử lý tiếp.

**check.py**: Sử dụng requests và selenium để kiểm tra danh sách URL từ urls.txt. Script này xác định các URL có chuyển hướng (redirect) và các URL không truy cập được, giúp làm sạch danh sách đầu vào.

**log.py**: Tự động đăng nhập vào các tài khoản Google được cung cấp, lấy mã App Password, và lưu lại dưới dạng email|app_password trong file mail.txt. App Password này rất cần thiết cho việc gửi email tự động.

**mail.py**: Đọc danh sách domain từ urls.txt và sử dụng các tài khoản email cùng App Password từ mail.txt để gửi báo cáo đến nhiều bên liên quan (như nhà đăng ký domain, ATTT, Bing/Microsoft, Cloudflare).

**chr.py**: Một công cụ mạnh mẽ để gửi báo cáo lên Google Safe Browsing. Script này có khả năng tự động mở URL, sử dụng tiện ích để chụp ảnh màn hình bằng chứng, upload ảnh và gửi báo cáo.

**ads.py**: Tự động truy cập các URL, tìm và click vào nút "Report abuse" (Báo cáo lạm dụng) trên trang web để báo cáo spam hoặc nội dung không phù hợp.

**vna.py**: Một script hữu ích để tự động tạo tài khoản Gmail mới, giúp bạn có thêm nguồn email để phục vụ cho các tác vụ báo cáo.

### Cài đặt và Chuẩn bị
**Cài đặt các thư viện Python:**
Mở terminal hoặc command prompt và chạy lệnh sau để cài đặt tất cả các thư viện cần thiết.

```bash
pip install selenium requests webdriver-manager rich urllib3 python-whois
```

---

### ✨Chuẩn bị các file đầu vào:

urls.txt: File này sẽ được tạo tự động khi bạn chạy sheet.py.

email.txt: Bạn cần tự tạo file này và điền các tài khoản Gmail theo định dạng email|password, mỗi dòng một tài khoản.

```bash
email_cua_ban_1@gmail.com|matkhau_cua_ban_1
email_cua_ban_2@gmail.com|matkhau_cua_ban_2
```
Chrome Driver: webdriver-manager sẽ tự động tải và quản lý Chrome Driver, bạn không cần phải làm thủ công.

**Cách Sử Dụng:**
Bạn nên thực hiện theo một luồng làm việc nhất định để đạt được hiệu quả tốt nhất.

**Tải danh sách domain:**
Chạy sheet.py để lấy danh sách domain mới nhất từ Google Sheet và lưu vào urls.txt.
```bash
python sheet.py
```
**Lấy App Password:**
Chạy log.py để tự động lấy App Password từ các tài khoản trong email.txt. Kết quả sẽ được lưu trong mail.txt.
```bash
python log.py
```
**Gửi báo cáo qua email:**
Sử dụng mail.py để gửi báo cáo hàng loạt đến các tổ chức liên quan.
```bash
python mail.py
```
**Báo cáo lên Google Safe Browsing:**
Chạy chr.py. Script sẽ hướng dẫn bạn qua các bước chọn nguồn domain, chế độ upload ảnh và số luồng chạy.
```bash
python chr.py
```
**Báo cáo lạm dụng trên website (tùy chọn):**
Chạy ads.py để tự động báo cáo trên các trang web có giao diện nút báo cáo tiêu chuẩn.
```bash
python ads.py
```
**Tạo tài khoản Gmail mới (tùy chọn):**
Nếu bạn cần thêm tài khoản email, chạy vna.py.
```bash
python vna.py
```
**Lưu ý: **Các script sử dụng Selenium có thể gặp lỗi nếu giao diện website thay đổi.
