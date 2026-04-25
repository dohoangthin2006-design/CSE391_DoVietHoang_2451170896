PHẦN A - KIỂM TRA ĐỌC HIỂU
Câu A1 - HTTP & Browser (Nguồn: 01_introduction_html_universe.md 1.1 Kiến trúc Client-Server, 1.2 HTTP, 1.3 Browser Rendering.)
1. Các bước khi truy cập https://shopee.vn
- DNS Lookup
shopee.vn → chuyển thành địa chỉ IP của server
- Thiết lập kết nối TCP
Trình duyệt tạo kết nối với server (3-way handshake)
- TLS Handshake (HTTPS)
Xác thực chứng chỉ SSL, thiết lập kết nối mã hóa
- Gửi HTTP Request (GET)
Trình duyệt gửi request đến server Shopee
- Server xử lý và trả về HTTP Response
Server trả HTML + status code (ví dụ: 200 OK)
- Browser parse HTML
Trình duyệt đọc cấu trúc HTML
- Tải tài nguyên phụ (CSS, JS, ảnh)
Gửi thêm nhiều request khác
- Render trang web
Tạo DOM + CSSOM → hiển thị giao diện

---
2. TabNetwork trong DevTools
TabNetwork hiển thị:
-Danh sách tất cả request (HTML, CSS, JS, image…)
-Status Code (200, 404, 500…)
-Time / Duration (thời gian load từng request)
-Waterfall (timeline tải tài nguyên)
-Size (dung lượng file)
-Type (document, stylesheet, script…)
Screenshot

Câu A2 - Semantic HTML(Nguồn: 04_visible_part_html.md)
Trang web bị Google đánh giá SEO thấp vì:
-dùng <div class="header"> thay vì <header> cho phần đầu trang.
-dùng <div class="nav"> thay vì <nav> cho phần điều hướng.
-dùng <div class="main"> thay vì <main> cho phần nội dung chính.
-dùng <div class ="product"> thay vì <article> cho phần sản phẩm.
-dùng <div class="footer"> thay vì <footer> cho phần chân trang.
=> Google không hiểu cấu trúc

Câu A3 - Block vs Inline
[ Hộp 1 ] (div gom các phần tử lại 1 khối)
Text A Text B (span gom các phần tử lại 1 dòng)
[ Hộp 2 ]
Text C Text D(text D in đậm(strong))
[ Hộp 3 ]

Câu A4 - Table
thead: tiêu đề cột
tbody: dữ liệu chính
tfoot: tổng kết
Lý do không nên dùng table để tạo layout cho trang web:
1. Không phải thẻ semantic => Google không hiểu cấu trúc.
2. Khó responsive(table khó co giãn linh hoạt theo màn hình)
3. Ảnh hưởng đến SEO (Screenreader sẽ hiểu nhầm là bảng dữ liệu)

PHẦN C - SUY LUẬN
Câu C1 - Thiết kế cấu trúc

<header> <!-- header cho phần đầu trang -->
    <nav> <!-- nav cho menu chính -->
        <a href="#home">Trang chủ</a>
    </nav>
</header>
<nav aria-label="Breadcrumb"> <!-- điều hướng -->
    <ol> <!-- ol là ordered list(xếp theo thứ tự) -->
        <li><a href="#home">Trang chủ</a></li>
        <li><a href="#iphone">Điện thoại</a></li>
        <li>iPhone 16</li>
    </ol>
</nav>
<main> <!-- main cho nội dung chính -->
    <section> <!-- section cho khu vực ảnh -->
        <figure> <!-- figure cho media với caption -->
            <img src="img1.jpg" alt="iPhone 16">
            <img src="img2.jpg" alt="iPhone 16">
            <img src="img3.jpg" alt="iPhone 16">
            <img src="img4.jpg" alt="iPhone 16">
            <img src="img5.jpg" alt="iPhone 16">
        </figure>
    </section>
    <section> <!-- section cho thông tin -->
        <h1>iPhone 16</h1>
        <p>25.990.000đ</p>
        <p>Đánh giá sao</p>
        <p>Mô tả</p>
    </section>
    <section> <!-- section cho bảng thông số kỹ thuật -->
        <table>
            <thead><tr><th>Thông số</th><th>Giá trị</th></tr></thead><!-- tr là table row, th là table header -->
            <tbody>...</tbody>
        </table>
    </section>
    <section> <!-- section cho đánh giá -->
        <article> <!-- article cho mỗi comment -->
            <p>Đánh giá</p>
        </article>
    </section>
</main>
<aside> <!-- aside cho sidebar -->
    <h3>Sản phẩm tương tự</h3>
    <article>...</article>
</aside>
<footer> <!-- footer cho cuối trang -->
    <p>&copy; 2026</p>
</footer>

Câu C2 - So sánh & Tranh luận
Quan điểm “chỉ dùng <div> + class là đủ” nghe có vẻ nhanh, nhưng bỏ qua nhiều lợi ích kỹ thuật quan trọng của semantic HTML.

    Thứ nhất, về SEO: các thẻ semantic như <header>, <main>, <article>, <nav> giúp công cụ tìm kiếm hiểu cấu trúc trang tốt hơn. Khi crawler đọc một trang, nó không “đoán” nội dung quan trọng dựa vào class, mà ưu tiên các thẻ có ý nghĩa. Ví dụ, nội dung nằm trong <article> hoặc tiêu đề <h1> sẽ được đánh giá cao hơn so với một <div> vô nghĩa.
    
    Thứ hai, về Accessibility: semantic HTML hỗ trợ tốt cho screen reader. Người khiếm thị sử dụng phần mềm đọc màn hình có thể nhanh chóng điều hướng qua <nav>, bỏ qua <footer>, hoặc nhảy tới <main>. Nếu chỉ dùng <div>, tất cả đều trở thành “khối chung chung”, khiến trải nghiệm kém đi rõ rệt.
    
    Ví dụ cụ thể: một trang tin tức. Nếu dùng <article> cho từng bài viết và <h2> cho tiêu đề, screen reader có thể liệt kê danh sách bài viết để người dùng chọn. Nếu thay bằng <div class="post">, công cụ hỗ trợ sẽ không hiểu đó là nội dung độc lập, làm giảm khả năng truy cập.
    
    Tuy nhiên, <div> vẫn rất cần thiết trong thực tế. Nó phù hợp khi bạn chỉ cần chia layout hoặc nhóm phần tử không mang ý nghĩa nội dung, ví dụ wrapper để dùng CSS Grid/Flexbox, hoặc container cho component UI.
    
    Tóm lại, semantic HTML không phải “tốn thời gian”, mà là đầu tư giúp code dễ hiểu hơn, thân thiện hơn với máy và người.

Câu B3:
    Lỗi 1: Dòng 1 - Thiếu html trong DOCTYPE.
    Lỗi 2: Dòng 2 - Thiếu language, thêm lang = "vi".
    Lỗi 3: Dòng 4 - Title chưa đóng.
    Lỗi 4: Dòng 5 - charset sai phải là UTF-8.
    Lỗi 5: Dòng 6 - Thiếu meta viewport.
    Lỗi 6: Dòng 8 - Thẻ đóng h1 thiếu /.
    Lỗi 7: Dòng 12 - Thẻ đóng a thiếu /.
    Lỗi 8: Dòng 20 - Thiếu "" ở src và thiếu alt.
    Lỗi 9: Dòng 22 - Thẻ <p> phải đóng ngoài cùng. Thẻ <b> đóng sai và ko phải thẻ semantic, đổi thành <strong>.
    Lỗi 10: Dòng 28-35 - Thiếu thead, tbody(phải đóng lại thead ở 28 và 31, tbody ở 32 và 35).
    Lỗi 11: Dòng 40 - Thừa main đổi thành aside.
    Lỗi 12: Dòng 45 - Thẻ đóng p thiếu /.

Câu B4:
    1. Trong ảnh shopee ta có thể thấy có rất ít semantic do chủ yếu là script nhưng thông thường chúng ta có thể thấy các thẻ semantic như header, footer,..
    Ngoài ra ta có thể thấy có những thẻ có thể dùng semantic nhưng lại dùng div trong ảnh như: div id = "main" hay div id = "modal" có thể sửa thành <main> và <dialog>
    2. Searchbar trong ảnh ko còn sử dụng table mà sử dụng flex
    3. Không thấy action và method, input types được dùng bao gồm:
    <input 
      class="shopee-searchbar-input__input"
      placeholder="Tìm sản phẩm, thương hiệu, và tên shop"
      maxlength="128"
      autocomplete="off"
      role="combobox"
    >