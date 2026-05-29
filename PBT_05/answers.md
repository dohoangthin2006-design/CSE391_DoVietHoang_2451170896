### PHẦN A - KIỂM TRA ĐỌC HIỂU
## Câu A1 - Viewport & Mobile-First
1. Thẻ <meta viewport> chuẩn:

<meta name="viewport" content="width=device-width, initial-scale=1.0">

Giải thích thuộc tính:

- name="viewport" : thuộc tính này chỉ thị cấu hình viewport của trang web.
- content="width=device-width" : chiều rộng của trang web tuân theo chiều rộng màn hình của thiết bị thực tế.
- content="initial-scale=1.0" : đặt mức độ thu phóng (zoom) ban đầu khi trang web vừa load xong.

2. Nếu thiếu thẻ này, iPhone giả định trang rộng 980px (như desktop) → thu nhỏ lại → chữ bé xíu → UX tệ.

3. Sự khác nhau giữa Mobile-First và Desktop-First

| Đặc điểm            | Mobile-First                                           | Desktop-First                                            |
|---------------------|--------------------------------------------------------|----------------------------------------------------------|
| Điểm bắt đầu        | Viết CSS cho màn hình nhỏ trước (Mobile)               |Viết CSS cho màn hình lớn trước (Desktop).                |
| Hướng mở rộng       | Thêm code để tối ưu khi màn hình to dần lên            |Thêm code để tối ưu khi màn hình nhỏ dần đi.              |
| Media Query sử dụng | Chủ yếu dùng min-width (áp dụng từ độ rộng này trở lên)|Chủ yếu dùng max-width (áp dụng từ độ rộng này trở xuống).|

Ví dụ CSS:

Mobile-First

/* Mặc định cho mobile (màn hình nhỏ) */
.container {
    width: 100%;
}

.product-grid {
    grid-template-columns: 1fr;
}

/* Tablet trở lên */
@media (min-width: 768px) {
    .product-grid { grid-template-columns: repeat(2, 1fr); }
}

Desktop-First

/* Mặc định cho desktop */
.product-grid { grid-template-columns: repeat(4, 1fr); }

/* Tablet */
@media (max-width: 1023px) {
    .product-grid { grid-template-columns: repeat(2, 1fr); }
}

Lý do Mobile-First tốt hơn:

- Mobile tải ít CSS hơn (mobile chỉ tải mobile styles, không download desktop styles)
- Buộc bạn ưu tiên nội dung quan trọng trước (content thinking)
- Google và performance tools đánh giá cao hơn

## Câu A2 - Breakpoints 

| Breakpoints | Kích thước    | Thiết bị                      | grid sản phẩm |
|-------------|---------------|-------------------------------|---------------|
| xs          | <576px        | Điện thoại dọc                | 1 đến 2 cột   |
| sm          | 576px - 767px | Điện thoại ngang              | 2 cột         |
| md          | 768px - 991px | Máy tính bảng                 | 3 cột         |
| lg          | 992px - 1199px| Máy tính bảng lớn/Laptop nhỏ  | 4 cột         |
| xl          | >= 1200px     | Màn hình desktop thông thường | 4 đến 5 cột   |

## Câu A3 - Media Queries

| Chiều rộng màn hình | `.container` width |
|---------------------|--------------------|
| 375px (iPhone SE)   | 100%               |
| 600px               | 540px              |
| 800px               | 720px              |
| 1000px              | 960px              |
| 1400px              | 1140px             |

## Câu A4 - SCSS Basics

1. Variables ($primary-color)

Tính năng chính: Khi muốn thay đổi giao diện, chỉ cần sửa giá trị của biến đó một lần duy nhất.

Ví dụ:

$primary-color: #ff5722;
$text-color: #333333;
$border-radius: 8px;

.button {
  background-color: $primary-color;
  color: #ffffff;
  border-radius: $border-radius;
  padding: 10px 20px;
}

.card {
  color: $text-color;
  border: 1px solid $primary-color;
  border-radius: $border-radius;
}

2. Nesting (viết CSS lồng nhau)

Tính năng chính: Thay vì phải viết đi viết lại bộ chọn cha (selector) như trong CSS thuần, có thể viết các bộ chọn con lồng trực tiếp vào bên trong bộ chọn cha, cấu trúc y hệt như sơ đồ HTML.

Ví dụ:

.navbar {
  background-color: #333;
  padding: 10px;

  ul {
    list-style: none;
    display: flex;
    li {
      margin-right: 20px;
      a {
        color: white;
        text-decoration: none;
        &:hover {
          color: #ff5722;
        }
      }
    }
  }
}

3. Mixins (@mixin, @include)

Tính năng chính: cho phép gom một nhóm các thuộc tính CSS được dùng đi dùng lại nhiều lần vào một chỗ, sau đó "gọi" nó ra ở bất kỳ class nào mà không cần phải gõ lại.

Ví dụ:

@mixin center-flex {
  display: flex;
  justify-content: center;
  align-items: center;
}

.box-header {
  height: 60px;
  background-color: #f5f5f5;
  @include center-flex;
}

.modal-content {
  width: 400px;
  height: 300px;
  @include center-flex;
}

4. @extend / Inheritance

Tính năng chính: cho phép một class chia sẻ/dùng chung toàn bộ các thuộc tính CSS của một class khác. Điều này giúp tránh việc phải viết lặp đi lặp lại các đoạn code giống nhau, hoặc phải gắn quá nhiều class vào một thẻ HTML.

Ví dụ:

.alert-base {
  padding: 15px;
  margin-bottom: 20px;
  border: 1px solid transparent;
  border-radius: 4px;
  font-weight: bold;
}

.alert-success {
  @extend .alert-base;
  background-color: #d4edda;
  color: #155724;
  border-color: #c3e6cb;
}

.alert-danger {
  @extend .alert-base;
  background-color: #f8d7da;
  color: #721c24;
  border-color: #f5c6cb;
}

Tại sao trình duyệt KHÔNG đọc được file .scss? Cần bước gì để chuyển SCSS → CSS?

SCSS không phải là ngôn ngữ tiêu chuẩn của web

Các bước để chuyển SCSS -> CSS:
VS Code: install extension Live Sass Compiler -> click Watch Sass
Terminal: cài thư viện Sass bằng lệnh: npm install -g sass
          sass --watch input.scss output.css
Vite, Webpack, hoặc Turbopack: tự động trong React, Vue, Next.js

### PHẦN C - PHÂN TÍCH
## Câu C1 - Phân tích trang web thực
- Navigation thay đổi thế nào? (hamburger? dropdown?)

Không thay đổi về cấu trúc, không có hamburger và dropdown

- Lưới content thay đổi mấy cột?

Không có sự thay đổi

- Elements nào bị ẩn trên mobile?

Không có elements nào bị ẩn

- Font size có thay đổi không?

Không thay đổi

## Câu C2 - Thiết kế Responsive Strategy

Mobile - 360px

┌─────────────────────────┐
│   LOGO        ☰  📞   │  
├─────────────────────────┤
│                         │
│     HERO IMAGE          │  
│   "Đặt bàn hôm nay  "   │
│      [ĐẶT BÀN]         │
│                         │
├─────────────────────────┤
│  Ảnh 1  │  Ảnh 2  │
├────────────┼────────────┤  
│  Ảnh 3  │  Ảnh 4  │
├────────────┼────────────┤
│   Ảnh 5  │  Ảnh 6  │
├─────────────────────────┤
│   Ngày:  [__________] │
│   Giờ:   [__________] │  
│   Số người: [_______] │
│   Ghi chú:            │
│  [___________________]  │
│                         │
│    [ ĐẶT BÀN NGAY ]    │
├─────────────────────────┤
│                         │
│      GOOGLE MAPS      │  
│     (full width)        │
│                         │
├─────────────────────────┤
│   Nhà hàng |  SĐT   │  
└─────────────────────────┘

Tablet - 768px

┌──────────────────────────────────────────────┐
│   LOGO              📞 0901 234 567        │  
├──────────────────────────────────────────────┤
│                                              │
│             HERO IMAGE                       │  
│         "Ẩm thực tinh tế"                   │
│           [ĐẶT BÀN NGAY]                    │
│                                              │
├──────────────────────────────────────────────┤
│   Ảnh 1  │   Ảnh 2  │   Ảnh 3        │
├────────────┼────────────┼────────────────────┤  
│   Ảnh 4  │   Ảnh 5  │  Ảnh 6        │
├─────────────────────────┬────────────────────┤
│  FORM ĐẶT BÀN (60%)    │  🗺 GOOGLE MAPS   │
│                         │   (40%)            │
│  [Ngày]   [Giờ  ]      │                    │  
│  [Số người]             │   sticky sidebar   │
│  [Ghi chú............]  │                    │
│                         │                    │
│     [ ĐẶT BÀN ]        │                    │
├────────────┬────────────┴────────────────────┤
│  Liên hệ  │  Giờ mở cửa                     │  
└────────────┴─────────────────────────────────┘

Desktop - 1280px

┌──────────────────────────────────────────────────────────────────┐
│  🍽 LOGO    Menu  Thực đơn  Về chúng tôi    📞 0901 234 567     │  
├──────────────────────────────────────────────────────────────────┤
│                                                                  │
│                                                                  │
│                    HERO IMAGE (100vh)                            │  
│               "Tinh hoa ẩm thực Việt Nam"                       │
│                    [ ĐẶT BÀN NGAY ]                             │
│                   ↓ scroll to explore                            │
│                                                                  │
│                                                                  │
├──────────────────────────────────────────────────────────────────┤
│  ┌──────────┐  ┌──────────┐  ┌──────────┐                       │
│  │  Ảnh 1 │  │  Ảnh 2 │  │  Ảnh 3 │                       │  
│  └──────────┘  └──────────┘  └──────────┘                       │    
│  ┌──────────┐  ┌──────────┐  ┌──────────┐                       │
│  │  Ảnh 4 │  │  Ảnh 5 │  │  Ảnh 6 │                       │
│  └──────────┘  └──────────┘  └──────────┘                       │
├──────────────────────────────────┬───────────────────────────────┤
│  FORM ĐẶT BÀN (60%)              │  🗺 GOOGLE MAPS (40%)         │
│                                  │                               │
│  [ Ngày] [ Giờ] [ Người]    │                               │  
│  [ Ghi chú.................. ] │   sticky, height khớp form    │
│                    [ĐẶT BÀN ▶]   │                               │
│                                  │                               │
├──────────┬──────────┬────────────┴──────────────────────────────┤
│   Logo  │ Liên hệ │ Giờ mở cửa  │  Facebook Instagram Zalo    │  
│  Slogan  │ ☎ Địa chỉ│ T2–CN       │                              │
└──────────┴──────────┴─────────────┴──────────────────────────────┘

CSS Skeleton (Mobile-First)

/* ── Breakpoints ─────────────────── */
/* mobile  : < 768px  (default)       */
/* tablet  : >= 768px                 */
/* desktop : >= 1024px                */

/* 1. HEADER */
.site-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
}
.header__nav       { display: none; }
.header__hamburger { display: flex; }

@media (min-width: 1024px) {
  .header__nav       { display: flex; }
  .header__hamburger { display: none; }
}

/* 2. HERO */
.hero { height: 50vh; }

@media (min-width: 768px)  { .hero { height: 60vh;  } }
@media (min-width: 1024px) { .hero { height: 100vh; } }

/* 3. FOOD GRID */
.food-grid {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 1rem;
}

@media (min-width: 768px) {
  .food-grid {
    grid-template-columns: repeat(3, 1fr);
  }
}

/* 4. BOOKING SECTION — form + map */
.booking-section {
  display: grid;
  grid-template-columns: 1fr;
  grid-template-areas:
    "form"
    "map";
}

@media (min-width: 768px) {
  .booking-section {
    grid-template-columns: 3fr 2fr;
    grid-template-areas: "form map";
  }
  .booking-map { position: sticky; top: 80px; }
}

/* 4a. Form fields layout */
.booking-form {
  grid-area: form;
  display: grid;
  grid-template-columns: 1fr;
}

@media (min-width: 768px) {
  .booking-form {
    grid-template-columns: 1fr 1fr;
  }
  .booking-form__note,
  .booking-form__submit { grid-column: 1 / -1; }
}

@media (min-width: 1024px) {
  .booking-form {
    grid-template-columns: repeat(4, 1fr);
  }
  .booking-form__note   { grid-column: 1 / 4; }
  .booking-form__submit { grid-column: 4 / 5; align-self: end; }
}

/* 4b. Map */
.booking-map { grid-area: map; }

/* 5. FOOTER */
.site-footer {
  display: grid;
  grid-template-columns: 1fr;
}

@media (min-width: 768px) {
  .site-footer { grid-template-columns: repeat(2, 1fr); }
}

@media (min-width: 1024px) {
  .site-footer { grid-template-columns: 2fr 1fr 1fr 1fr; }
}