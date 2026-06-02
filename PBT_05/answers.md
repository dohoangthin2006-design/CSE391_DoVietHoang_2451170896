# PHẦN A — KIỂM TRA ĐỌC HIỂU

---

# Câu A1 — Viewport & Mobile-First

## 1. Thẻ `<meta viewport>` chuẩn

```html id="owkn34"
<meta
  name="viewport"
  content="width=device-width, initial-scale=1.0"
/>
```

---

## Giải thích thuộc tính

| Thuộc tính           | Ý nghĩa                                             |
| -------------------- | --------------------------------------------------- |
| `name="viewport"`    | Chỉ định cấu hình viewport cho trang web            |
| `width=device-width` | Chiều rộng website bằng chiều rộng thiết bị thực tế |
| `initial-scale=1.0`  | Mức zoom mặc định khi trang vừa load                |

---

## 2. Nếu thiếu thẻ viewport

iPhone sẽ giả định trang web rộng khoảng `980px` như desktop.

Kết quả:

* Trang bị thu nhỏ lại
* Chữ rất nhỏ
* UX kém
* Responsive hoạt động không đúng

---

## 3. Mobile-First vs Desktop-First

| Đặc điểm      | Mobile-First                | Desktop-First               |
| ------------- | --------------------------- | --------------------------- |
| Điểm bắt đầu  | Viết CSS cho mobile trước   | Viết CSS cho desktop trước  |
| Hướng mở rộng | Tối ưu cho màn hình lớn dần | Tối ưu cho màn hình nhỏ dần |
| Media Query   | `min-width`                 | `max-width`                 |

---

## Ví dụ CSS

### Mobile-First

```css id="e8o40h"
/* Mặc định cho mobile */
.container {
  width: 100%;
}

.product-grid {
  grid-template-columns: 1fr;
}

/* Tablet trở lên */
@media (min-width: 768px) {
  .product-grid {
    grid-template-columns: repeat(2, 1fr);
  }
}
```

---

### Desktop-First

```css id="j9xjso"
/* Mặc định cho desktop */
.product-grid {
  grid-template-columns: repeat(4, 1fr);
}

/* Tablet */
@media (max-width: 1023px) {
  .product-grid {
    grid-template-columns: repeat(2, 1fr);
  }
}
```

---

## Vì sao Mobile-First tốt hơn?

* Mobile tải ít CSS hơn
* Ưu tiên nội dung quan trọng trước
* Tối ưu performance
* Google đánh giá tốt hơn
* Responsive dễ maintain hơn

---

# Câu A2 — Breakpoints

| Breakpoint | Kích thước       | Thiết bị                | Grid sản phẩm |
| ---------- | ---------------- | ----------------------- | ------------- |
| `xs`       | `<576px`         | Điện thoại dọc          | 1–2 cột       |
| `sm`       | `576px - 767px`  | Điện thoại ngang        | 2 cột         |
| `md`       | `768px - 991px`  | Máy tính bảng           | 3 cột         |
| `lg`       | `992px - 1199px` | Laptop nhỏ / tablet lớn | 4 cột         |
| `xl`       | `>=1200px`       | Desktop                 | 4–5 cột       |

---

# Câu A3 — Media Queries

| Chiều rộng màn hình | `.container` width |
| ------------------- | ------------------ |
| `375px` (iPhone SE) | `100%`             |
| `600px`             | `540px`            |
| `800px`             | `720px`            |
| `1000px`            | `960px`            |
| `1400px`            | `1140px`           |

---

# Câu A4 — SCSS Basics

## 1. Variables (`$primary-color`)

### Ý nghĩa

Cho phép tái sử dụng giá trị nhiều lần và chỉ cần sửa ở một nơi.

---

### Ví dụ

```scss id="0hr38j"
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
```

---

## 2. Nesting

### Ý nghĩa

Cho phép viết CSS lồng nhau giống cấu trúc HTML.

---

### Ví dụ

```scss id="rbw5m5"
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
```

---

## 3. Mixins (`@mixin`, `@include`)

### Ý nghĩa

Tái sử dụng nhiều đoạn CSS giống nhau.

---

### Ví dụ

```scss id="fiyjj1"
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
```

---

## 4. `@extend` / Inheritance

### Ý nghĩa

Cho phép class dùng lại toàn bộ thuộc tính của class khác.

---

### Ví dụ

```scss id="vl22jm"
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
```

---

## Vì sao trình duyệt không đọc được file `.scss`?

SCSS không phải ngôn ngữ tiêu chuẩn mà browser hiểu trực tiếp.

Trình duyệt chỉ đọc được CSS.

Vì vậy cần compile:

```text id="ynnhjg"
SCSS → CSS
```

---

## Các cách compile SCSS

### VS Code

* Cài extension: `Live Sass Compiler`
* Chọn `Watch Sass`

---

### Terminal

Cài Sass:

```bash id="u8g8eh"
npm install -g sass
```

Compile:

```bash id="4af2vz"
sass --watch input.scss output.css
```

---

### Frameworks

Các framework như:

* React
* Vue
* Next.js
* Vite
* Webpack
* Turbopack

có thể tự động compile SCSS.

---

# PHẦN C — PHÂN TÍCH

# Câu C1 — Phân tích trang web thực

## Navigation thay đổi thế nào?

* Không thay đổi cấu trúc
* Không có hamburger menu
* Không có dropdown

---

## Lưới content thay đổi mấy cột?

* Không có sự thay đổi

---

## Elements nào bị ẩn trên mobile?

* Không có element nào bị ẩn

---

## Font size có thay đổi không?

* Không thay đổi

---

# Câu C2 — Thiết kế Responsive Strategy

## Mobile — 360px

```text id="m83c2u"
┌─────────────────────────┐
│   LOGO        ☰   📞    │
├─────────────────────────┤
│                         │
│       HERO IMAGE        │
│    "Đặt bàn hôm nay"    │
│      [ ĐẶT BÀN ]        │
│                         │
├─────────────────────────┤
│   Ảnh 1   │   Ảnh 2     │
├───────────┼─────────────┤
│   Ảnh 3   │   Ảnh 4     │
├───────────┼─────────────┤
│   Ảnh 5   │   Ảnh 6     │
├─────────────────────────┤
│  Ngày:     [_______]    │
│  Giờ:      [_______]    │
│  Số người: [_______]    │
│  Ghi chú:               │
│  [__________________]   │
│                         │
│    [ ĐẶT BÀN NGAY ]     │
├─────────────────────────┤
│                         │
│       GOOGLE MAPS       │
│       (full width)      │
│                         │
├─────────────────────────┤
│   Nhà hàng  |   SĐT     │
└─────────────────────────┘
```

---

## Tablet — 768px

```text id="n3wq6w"
┌──────────────────────────────────────────────┐
│   LOGO             📞 0901 234 567           │
├──────────────────────────────────────────────┤
│                                              │
│               HERO IMAGE                     │
│            "Ẩm thực tinh tế"                │
│             [ ĐẶT BÀN NGAY ]                │
│                                              │
├──────────────────────────────────────────────┤
│  Ảnh 1 │ Ảnh 2 │ Ảnh 3                      │
├────────┼────────┼────────────────────────────┤
│  Ảnh 4 │ Ảnh 5 │ Ảnh 6                      │
├─────────────────────────┬────────────────────┤
│ FORM ĐẶT BÀN (60%)      │ GOOGLE MAPS (40%) │
│                         │                    │
│ [Ngày]    [Giờ]         │ sticky sidebar    │
│ [Số người]              │                    │
│ [Ghi chú.............]  │                    │
│                         │                    │
│      [ ĐẶT BÀN ]        │                    │
├────────────┬────────────┴────────────────────┤
│ Liên hệ    │ Giờ mở cửa                     │
└────────────┴─────────────────────────────────┘
```

---

## Desktop — 1280px

```text id="0ynszk"
┌────────────────────────────────────────────────────────────────┐
│ 🍽 LOGO  Menu  Thực đơn  Về chúng tôi   📞 0901 234 567       │
├────────────────────────────────────────────────────────────────┤
│                                                                │
│                    HERO IMAGE (100vh)                          │
│              "Tinh hoa ẩm thực Việt Nam"                      │
│                   [ ĐẶT BÀN NGAY ]                             │
│                  ↓ scroll to explore                           │
│                                                                │
├────────────────────────────────────────────────────────────────┤
│ ┌──────────┐ ┌──────────┐ ┌──────────┐                         │
│ │  Ảnh 1   │ │  Ảnh 2   │ │  Ảnh 3   │                         │
│ └──────────┘ └──────────┘ └──────────┘                         │
│ ┌──────────┐ ┌──────────┐ ┌──────────┐                         │
│ │  Ảnh 4   │ │  Ảnh 5   │ │  Ảnh 6   │                         │
│ └──────────┘ └──────────┘ └──────────┘                         │
├──────────────────────────────────┬─────────────────────────────┤
│ FORM ĐẶT BÀN (60%)               │ GOOGLE MAPS (40%)          │
│                                  │                             │
│ [Ngày] [Giờ] [Người]             │ sticky sidebar             │
│ [Ghi chú......................]  │                             │
│                     [ĐẶT BÀN ▶] │                             │
│                                  │                             │
├──────────┬──────────┬────────────┴─────────────────────────────┤
│ Logo     │ Liên hệ  │ Giờ mở cửa │ Facebook Instagram Zalo    │
│ Slogan   │ ☎ Địa chỉ│ T2–CN       │                             │
└──────────┴──────────┴──────────────────────────────────────────┘
```

---

## CSS Skeleton (Mobile-First)

```css id="z2wc5l"
/* ───────────────────────────── */
/* Breakpoints                   */
/* mobile  : <768px (default)    */
/* tablet  : >=768px             */
/* desktop : >=1024px            */
/* ───────────────────────────── */

/* 1. HEADER */

.site-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.header__nav {
  display: none;
}

.header__hamburger {
  display: flex;
}

@media (min-width: 1024px) {
  .header__nav {
    display: flex;
  }

  .header__hamburger {
    display: none;
  }
}

/* 2. HERO */

.hero {
  height: 50vh;
}

@media (min-width: 768px) {
  .hero {
    height: 60vh;
  }
}

@media (min-width: 1024px) {
  .hero {
    height: 100vh;
  }
}

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

/* 4. BOOKING SECTION */

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

  .booking-map {
    position: sticky;
    top: 80px;
  }
}

/* 4a. FORM */

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
  .booking-form__submit {
    grid-column: 1 / -1;
  }
}

@media (min-width: 1024px) {
  .booking-form {
    grid-template-columns: repeat(4, 1fr);
  }

  .booking-form__note {
    grid-column: 1 / 4;
  }

  .booking-form__submit {
    grid-column: 4 / 5;
    align-self: end;
  }
}

/* 4b. MAP */

.booking-map {
  grid-area: map;
}

/* 5. FOOTER */

.site-footer {
  display: grid;
  grid-template-columns: 1fr;
}

@media (min-width: 768px) {
  .site-footer {
    grid-template-columns: repeat(2, 1fr);
  }
}

@media (min-width: 1024px) {
  .site-footer {
    grid-template-columns: 2fr 1fr 1fr 1fr;
  }
}
```
