PHẦN A — KIỂM TRA ĐỌC HIỂU

Câu A1 - Input Types

1. type="text" → Ô nhập thông thường → minlength, maxlength, pattern → Nhập tên khách hàng

2. type="email" → Ô nhập email → Kiểm tra định dạng @ → Đăng ký tài khoản

3. type="password" → Ký tự bị ẩn → minlength, pattern → Nhập mật khẩu

4. type="number" → Có nút tăng/giảm → min, max, step → Chọn số lượng sản phẩm

5. type="tel" → Hiện bàn phím số trên mobile → pattern → Nhập số điện thoại

6. type="date" → Date picker → min, max → Chọn ngày giao hàng

7. type="file" → Chọn file → accept, multiple → Upload ảnh sản phẩm

8. type="search" → Ô tìm kiếm có nút x → Không có validation đặc biệt → Tìm kiếm sản phẩm

9. type="checkbox" → Chọn có/không → required → Đồng ý điều khoản

10. type="radio" → Chọn một trong nhiều → required → Chọn phương thức thanh toán

Câu A2 - Validation Attributes

<!-- Trường hợp 1 -->

<input type="text" required value=""> <!-- User để trống --> không submit được vì thuộc tính required bắt buộc người dùng phải nhập dữ liệu

<!-- Trường hợp 2 -->

<input type="email" value="abc"> <!-- User gõ "abc" --> không submit được vì không đúng định dạng (không chứa ký tự @ và domain)

<!-- Trường hợp 3 -->

<input type="number" min="1" max="10" value="15"> <!-- User gõ 15 --> không submit được vì giá trị 15 vượt quá max="10"

<!-- Trường hợp 4 -->

<input type="text" pattern="[0-9]{10}" value="abc123"> <!-- User gõ "abc123" --> không submit được vì chứa chữ cái

<!-- Trường hợp 5 -->

<input type="password" minlength="8" value="123"> <!-- User gõ "123" --> không submit được vì chưa đạt số ký tự tối thiểu minlength="8"

Câu A3 - Accessibility

1. Tại sao <label for="email"> quan trọng cho người dùng screen reader?

giúp Screen reader biết ô input đó cần nhập email và click vào label

2. Khi nào dùng <fieldset> + <legend>? Cho ví dụ cụ thể.

dùng khi nhóm các input liên quan đến nhau. Screen reader sẽ hiểu đây là cùng một nhóm thông tin. Ví dụ: Thông tin giao hàng

<fieldset>
    <legend>Thông tin giao hàng</legend>
    <label for="street">Đường:</label>
    <input type="text" id="street" name="street">
</fieldset>

3. aria-label dùng khi nào? Tại sao KHÔNG nên dùng aria-label khi đã có <label>?

aria-label được dùng khi một phần tử không có text hiển thị rõ ràng nhưng vẫn cần screen reader hiểu chức năng của nó.

không nên dùng aria-label khi đã có <label> vì có thể bị trùng nội dung

Câu A4 - Media

1. Giải thích thuộc tính loading="lazy" trên thẻ <img>. Nó cải thiện gì? Khi nào KHÔNG nên dùng?

thuộc tính loading="lazy" dùng để trì hoãn việc tải ảnh cho tới khi ảnh gần xuất hiện trong vùng nhìn thấy của người dùng.

Nó giúp:

- Giảm dung lượng tải ban đầu

- Tăng tốc độ mở trang

- Giảm băng thông

Không nên dùng cho banner đầu trang, các logo quan trọng, các ảnh cần phải xuất hiện ngay khi mở trang.

2. Tại sao nên cung cấp nhiều <source> trong thẻ <video>? Liệt kê ít nhất 3 format video web phổ biến.

nên cung cấp nhiều <source> trong thẻ <video> vì không phải trình duyệt nào cũng hỗ trợ cùng một định dạng video

Ví dụ:

<video controls>
    <source src="movie.mp4" type="video/mp4">
    <source src="movie.webm" type="video/webm">
    <source src="movie.ogv" type="video/ogg">
</video>

3. Thuộc tính alt trên <img> dùng để làm gì? Viết alt tốt cho 3 trường hợp:
   Ảnh sản phẩm iPhone 16
   Ảnh trang trí (decorative)
   Ảnh biểu đồ doanh thu Q1/2026

thuộc tính alt dùng để cung cấp văn bản mô tả cho hình ảnh.

<img src="https://cellphones.com.vn/sforum/can-canh-hinh-anh-iphone-16" alt="iPhone 16 Pro màu đen nhìn từ mặt trước">

<img src="https://vivahome.vn/khung-anh-treo-tuong-trang-tri-mau-trang-xanh-hai-quan?srsltid=AfmBOooX6hloGJ1GQUh_BMxOGYr8BabxQC7sA8QleDEH-VWve_EMb5su" alt="">

<img src="https://24hmoney.vn/news/hcm-q1-2026-chuyen-huong-than-trong-c30a2777383.html" alt="Biểu đồ doanh thu Q1 năm 2026 tăng từ tháng 1 đến tháng 3">

Câu A5 - So sánh <figure> vs <img>

<!-- Cách 1 -->
<img src="product.jpg" alt="iPhone">

đơn giản, ngắn gọn

<!-- Cách 2 -->
<figure>
    <img src="product.jpg" alt="iPhone 16 Pro Max 256GB Titan">
    <figcaption>iPhone 16 Pro Max — 25.990.000đ</figcaption>
</figure>

cho biết ảnh và caption liên quan đến nhau
cung cấp chú thích rõ ràng
Accessibility và SEO tốt hơn

Phần B - THỰC HÀNH CODE

Câu B1 - Form Đăng ký Tài khoản

HTML không thể validate confirm password vì với mỗi input nó chỉ kiểm tra giá trị được nhập vào của chính input đó và không thể truy cập được vào input khác nên không thể so sánh và confirm.

PHẦN C — PHÂN TÍCH & SUY LUẬN

Câu C1 — Debug Form

- Lỗi 1: Dòng 2 - Input tên không có <label for="...">, vi phạm accessibility

Sửa: <label for="name">Tên:</label>

- Lỗi 2: Dòng 2 - Input tên thiếu thuộc tính name và id

Sửa: <input type="text" id="name" name="name" required>

- Lỗi 3: Dòng 4 - Input email chỉ dùng placeholder, không có label

Sửa: <label for="email">Email:</label>
<input type="email" id="email" name="email" placeholder="Email của bạn" required>

- Lỗi 4: Dòng 6 - Input password không có label

Sửa: <label for="password">Mật khẩu:</label>
<input type="password" id="password" name="password" minlength="8" required>

- Lỗi 5: Dòng 7 - Ô nhập lại password không có label và không phân biệt với password chính

Sửa: <label for="confirm_password">Nhập lại mật khẩu:</label>
<input type="password" id="confirm_password" name="confirm_password" minlength="8" required>

- Lỗi 6: Dòng 9 - Phone dùng type="text" thay vì type="tel"

Sửa: <input type="tel" id="phone" name="phone" value="0901234567" required>

- Lỗi 7: Dòng 9 - Phone dùng value cố định thay vì placeholder

Sửa: <input type="tel" id="phone" name="phone" placeholder="0901234567" required>

- Lỗi 8: Dòng 11 -Select không có label

Sửa: <label for="city">Thành phố:</label>
<select id="city" name="city">

- Lỗi 9: Lỗi 9: Dòng 16-18 — Label điều khoản không liên kết với checkbox và còn thiếu checkbox

Sửa:
<input type="checkbox" id="terms" required>
<label for="terms">Tôi đồng ý điều khoản</label>

Câu C2 - Thiết kế chiến lược Validation

1. Viết pattern regex cho CMND/CCCD và Số tài khoản
   <input type="text" pattern="[0-9]{10,15}" required>
2. Giải thích: HTML5 validation đủ an toàn cho ứng dụng ngân hàng chưa? Tại sao?
   Không đủ an toàn.

HTML5 validation chỉ hoạt động ở frontend (trình duyệt người dùng). Người dùng có thể:

Tắt validation
Sửa HTML bằng DevTools
Gửi request trực tiếp bằng Postman/cURL
Bypass JavaScript và HTML validation

Vì vậy backend vẫn phải validate lại toàn bộ dữ liệu để đảm bảo bảo mật.

3. Liệt kê 3 loại validation mà HTML5 KHÔNG THỂ làm được (phải dùng JavaScript)

Kiểm tra “Nhập lại mật khẩu” có giống mật khẩu hay không
→ Cần JavaScript để so sánh 2 field

Kiểm tra email đã tồn tại trong database chưa
→ Phải gọi backend/API

Kiểm tra độ mạnh mật khẩu phức tạp
→ Ví dụ: phát hiện mật khẩu yếu, phổ biến, bị rò rỉ
→ Cần JavaScript hoặc backend xử lý

4. Nêu 2 rủi ro bảo mật nếu chỉ validate trên Frontend mà không validate Backend

- Người dùng bypass validation và gửi dữ liệu sai/độc hại
  → Có thể gây lỗi hệ thống hoặc tấn công injection

- Hacker gửi request giả trực tiếp tới server
  → Vì frontend validation có thể bị bỏ qua hoàn toàn
  → Dẫn tới rủi ro bảo mật và dữ liệu không hợp lệ
