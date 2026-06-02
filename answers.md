# CSS Frameworks — Bootstrap 5 / TailwindCSS

---

# PHẦN A — ĐỌC HIỂU

## Câu A1 — Grid System

### Code

```html
<div class="container">
  <div class="row">
    <div class="col-12 col-md-6 col-lg-3">Box 1</div>
    <div class="col-12 col-md-6 col-lg-3">Box 2</div>
    <div class="col-12 col-md-6 col-lg-3">Box 3</div>
    <div class="col-12 col-md-6 col-lg-3">Box 4</div>
  </div>
</div>
```

---

### Responsive Layout

| Kích thước màn hình | Layout            | Số cột |
| ------------------- | ----------------- | ------ |
| `< 768px`           | Các box xếp chồng | 1 cột  |
| `768px - 991px`     | Grid 2x2          | 2 cột  |
| `>= 992px`          | 1 hàng ngang      | 4 cột  |

---

### Giải thích class

- `col-12`
  - Box chiếm toàn bộ 12 cột trên mobile.

- `col-md-6`
  - Từ breakpoint `md` (`>=768px`) box chiếm 6/12 cột.
  - Mỗi hàng chứa 2 box.

- `col-lg-3`
  - Từ breakpoint `lg` (`>=992px`) box chiếm 3/12 cột.
  - Mỗi hàng chứa 4 box.

> Không cần viết `col-sm-12` vì `col-12` đã áp dụng cho mọi kích thước nhỏ hơn breakpoint tiếp theo.

---

### Layout minh họa

#### Mobile (`<768px`)

```text
┌─────────────┐
│   Box 1     │
├─────────────┤
│   Box 2     │
├─────────────┤
│   Box 3     │
├─────────────┤
│   Box 4     │
└─────────────┘
```

#### Tablet (`768px - 991px`)

```text
┌──────────┬──────────┐
│  Box 1   │  Box 2   │
├──────────┼──────────┤
│  Box 3   │  Box 4   │
└──────────┴──────────┘
```

#### Desktop (`>=992px`)

```text
┌────┬────┬────┬────┐
│ B1 │ B2 │ B3 │ B4 │
└────┴────┴────┴────┘
```

---

# Câu A2 — Utilities & Components

## 1. Giải thích `d-none d-md-block`

### Ý nghĩa

- `d-none`
  - `display: none`
  - Ẩn element.

- `d-md-block`
  - Từ breakpoint `md` (`>=768px`) hiển thị lại dưới dạng `display: block`.

---

### Hoạt động

| Kích thước màn hình | Trạng thái |
| ------------------- | ---------- |
| `<768px`            | Ẩn         |
| `>=768px`           | Hiện       |

---

## 2. Spacing Utilities

| Utility   | CSS tương đương               | Giá trị | Ý nghĩa               |
| --------- | ----------------------------- | ------- | --------------------- |
| `mt-3`    | `margin-top: 1rem;`           | 16px    | Khoảng cách phía trên |
| `px-4`    | `padding-left/right: 1.5rem;` | 24px    | Padding trái/phải     |
| `mb-auto` | `margin-bottom: auto;`        | auto    | Tự căn layout         |
| `py-2`    | `padding-top/bottom: 0.5rem;` | 8px     | Padding trên/dưới     |
| `ms-5`    | `margin-left: 3rem;`          | 48px    | Margin bên trái       |

---

## 3. So sánh `.container`, `.container-fluid`, `.container-md`

### `.container`

```html
<div class="container"></div>
```

#### Đặc điểm

- Có `max-width`
- Responsive theo breakpoint
- Tự căn giữa

#### Hoạt động

| Thiết bị | Width       |
| -------- | ----------- |
| Mobile   | 100%        |
| Desktop  | Có giới hạn |

#### Dùng khi

- Website thông thường
- Nội dung cần dễ đọc
- Layout không quá rộng

---

### `.container-fluid`

```html
<div class="container-fluid"></div>
```

#### Đặc điểm

- `width: 100%`
- Full chiều ngang màn hình

#### Dùng khi

- Banner full width
- Navbar full width
- Background kéo dài toàn màn hình

---

### `.container-md`

```html
<div class="container-md"></div>
```

#### Đặc điểm

- `<768px` → full width
- `>=768px` → giống `.container`

#### Hoạt động

| Kích thước | Width          |
| ---------- | -------------- |
| `<768px`   | 100%           |
| `>=768px`  | Có `max-width` |

---

# PHẦN C — PHÂN TÍCH

## Câu C1 — Tùy biến Bootstrap

## 1. Đổi `$primary` sang `#E63946`

### Công cụ cần dùng

| Công cụ          | Mục đích           |
| ---------------- | ------------------ |
| VS Code          | Chỉnh sửa file     |
| Sass Compiler    | Compile SCSS → CSS |
| Node.js + npm    | Quản lý package    |
| Browser DevTools | Kiểm tra CSS       |

---

### Không nên sửa trực tiếp

```text
node_modules/bootstrap/scss/_variables.scss
```

Vì sẽ bị ghi đè khi update Bootstrap.

---

### Cách đúng — Override bằng SCSS

### Cấu trúc thư mục

```text
src/
├── scss/
│   └── custom.scss
└── css/
    └── styles.css
```

---

### File `custom.scss`

```scss
$primary: #e63946;

@import "../../node_modules/bootstrap/scss/bootstrap";
```

---

### package.json

```json
{
  "scripts": {
    "sass": "sass src/scss/custom.scss src/css/styles.css",
    "sass:watch": "sass --watch src/scss:src/css"
  }
}
```

---

### Chạy compiler

```bash
npm run sass
```

---

### Link CSS vào HTML

```html
<link rel="stylesheet" href="src/css/styles.css" />
```

---

### Kết quả

Các class sau sẽ đổi màu:

- `.btn-primary`
- `.bg-primary`
- `.text-primary`
- `.alert-primary`
- `.border-primary`

---

### Lưu ý

- Khai báo `$primary` trước khi import Bootstrap.
- Không sửa trực tiếp trong `node_modules`.
- Sau khi sửa SCSS phải compile lại.

---

## 2. Vì sao không nên override `.btn-primary` trực tiếp?

### Cách không tốt

```css
.btn-primary {
  background: red !important;
}
```

### Vấn đề

- Phải dùng `!important`
- Khó maintain
- Dễ conflict CSS
- Phải sửa nhiều class khác nhau
- CSS bundle lớn hơn

---

### Cách đúng

```scss
$primary: #e63946;

@import "bootstrap/scss/bootstrap";
```

### Lợi ích

- Chỉ sửa 1 biến
- Bootstrap tự generate toàn bộ utility/component
- Không cần `!important`
- Maintain dễ hơn
- Tối ưu hơn

---

# Câu C2 — So sánh CSS Thuần và Bootstrap

## A. CSS Thuần

### Navbar HTML

```html
<nav class="navbar">
  <div class="navbar-brand">Logo</div>

  <ul class="navbar-menu">
    <li><a href="#">Home</a></li>
    <li><a href="#">About</a></li>
    <li><a href="#">Products</a></li>
  </ul>

  <button class="hamburger">☰</button>
</nav>
```

---

### Navbar CSS

```css
.navbar {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 1rem 2rem;
  background: #333;
  position: sticky;
  top: 0;
}

.navbar-brand {
  font-size: 1.5rem;
  color: white;
  font-weight: bold;
}

.navbar-menu {
  display: flex;
  list-style: none;
  gap: 2rem;
}

.navbar-menu a {
  color: white;
  text-decoration: none;
  transition: color 0.3s;
}

.navbar-menu a:hover {
  color: #ffaa00;
}

.hamburger {
  display: none;
  background: none;
  border: none;
  color: white;
  font-size: 1.5rem;
  cursor: pointer;
}

@media (max-width: 768px) {
  .navbar-menu {
    display: none;
    flex-direction: column;
    position: absolute;
    top: 60px;
    right: 0;
    background: #333;
    padding: 1rem;
    width: 100%;
  }

  .hamburger {
    display: block;
  }
}
```

**Số dòng CSS:** ~60 dòng

---

### Product Card HTML

```html
<div class="card">
  <img src="product.jpg" class="card-img" alt="Product" />

  <div class="card-body">
    <h5 class="card-title">Product Name</h5>

    <p class="card-description">Description...</p>

    <div class="card-footer">
      <span class="price">$29.99</span>
      <button class="btn btn-primary">Buy Now</button>
    </div>
  </div>
</div>
```

---

### Product Card CSS

```css
.card {
  border: 1px solid #ddd;
  border-radius: 8px;
  overflow: hidden;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  transition: box-shadow 0.3s;
  max-width: 300px;
}

.card:hover {
  box-shadow: 0 8px 16px rgba(0, 0, 0, 0.2);
}

.card-img {
  width: 100%;
  height: 250px;
  object-fit: cover;
}

.card-body {
  padding: 1rem;
}

.card-title {
  font-size: 1.25rem;
  font-weight: 600;
  margin-bottom: 0.5rem;
}

.card-description {
  font-size: 0.875rem;
  color: #666;
  margin-bottom: 1rem;
}

.card-footer {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.price {
  font-size: 1.5rem;
  font-weight: bold;
  color: #ff6600;
}

.btn-primary {
  background: #0066cc;
  color: white;
  border: none;
  padding: 0.5rem 1rem;
  border-radius: 4px;
  cursor: pointer;
}

.btn-primary:hover {
  background: #0052a3;
}
```

**Số dòng CSS:** ~50 dòng

---

## B. Bootstrap

### Navbar

```html
<nav class="navbar navbar-expand-lg navbar-dark bg-dark sticky-top">
  <div class="container-fluid">
    <a class="navbar-brand" href="#"> Logo </a>

    <button
      class="navbar-toggler"
      type="button"
      data-bs-toggle="collapse"
      data-bs-target="#navbarNav"
    >
      <span class="navbar-toggler-icon"></span>
    </button>

    <div class="collapse navbar-collapse" id="navbarNav">
      <ul class="navbar-nav ms-auto">
        <li class="nav-item">
          <a class="nav-link" href="#">Home</a>
        </li>

        <li class="nav-item">
          <a class="nav-link" href="#">About</a>
        </li>

        <li class="nav-item">
          <a class="nav-link" href="#">Products</a>
        </li>
      </ul>
    </div>
  </div>
</nav>
```

**CSS cần viết:** `0 dòng`

---

### Product Card

```html
<div class="card shadow-sm">
  <img src="product.jpg" class="card-img-top" alt="Product" />

  <div class="card-body">
    <h5 class="card-title">Product Name</h5>

    <p class="card-text">Description...</p>

    <div class="d-flex justify-content-between align-items-center">
      <span class="fs-5 fw-bold text-warning"> $29.99 </span>

      <button class="btn btn-primary">Buy Now</button>
    </div>
  </div>
</div>
```

**CSS cần viết:** `0 dòng`

---

## Bảng So Sánh

| Tiêu chí             | CSS Thuần           | Bootstrap    |
| -------------------- | ------------------- | ------------ |
| Dòng CSS cần viết    | ~110 dòng           | 0 dòng       |
| Thời gian phát triển | 2-3 giờ             | ~20 phút     |
| Responsive           | Tự viết media query | Có sẵn       |
| Grid System          | Tự code             | Có sẵn       |
| Navbar               | Tự xử lý            | Có component |
| Product Card         | Tự thiết kế         | Có sẵn       |
| Khả năng tùy biến    | Rất cao             | Bị giới hạn  |
| Performance          | Nhẹ hơn             | Nặng hơn     |
| Dễ maintain          | Khó hơn             | Dễ hơn       |
