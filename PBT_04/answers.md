### Câu A1 — 5 Loại Positioning

| Position   | Vẫn chiếm chỗ trong flow? | Tham chiếu vị trí     | Cuộn theo trang? | Use case                                    |
| ---------- | ------------------------- | --------------------- | ---------------- | ------------------------------------------- |
| `static`   | Có                        | Không dùng            | Có               | Mặc định                                    |
| `relative` | Có                        | Chính vị trí cũ       | Có               | Dịch chuyển nhẹ,làm cha cho absolute        |
| `absolute` | Không                     | Cha relative gần nhất | Có               | Badge, dropdown, tooltip, overlay           |
| `fixed`    | Không                     | Dính vào viewport     | Không            | Chat button, cookie banner, header cố định  |
| `sticky`   | Có                        | Viewport(khi dính)    | Một phần         | Sticky header, sticky table header, sidebar |

- absolute tham chiếu body khi không có cha position nào khác ngoài static, khi đó element bay ra khỏi flow và bám vào dưới body
- tham chiếu parent khi cha gần nhất có position là relative (hoặc absolute, fixed, sticky)
- khái niệm "nearest positioned ancestor" là cha gần nhất có position không phải static

### Câu A2 — Flexbox vs Grid

- Trường hợp 1 — flex: 1 (4 items)
  .container { display: flex } .item { flex: 1 }
  ┌───────────────────────────────┐
  │ Item1 │ Item2 │ Item3 │ Item4 │
  └───────────────────────────────┘
  1 hàng ngang, 4 cột bằng nhau — mỗi item chiếm 25% chiều rộng container

- Trường hợp 2 - flex-wrap: wrap, width: 45% (6 items)
  .container { display: flex; flex-wrap: wrap } .item { width: 45%; margin: 2.5% }
  ┌────────────────────────────────┐
  │ Item1 (45%) │ Item2 (45%) │
  │ Item3 (45%) │ Item4 (45%) │
  │ Item5 (45%) │ Item6 (45%) │
  └────────────────────────────────┘
  3 hàng × 2 cột. Mỗi item = 45% + 2×2.5% margin = 50% → vừa đúng 2 item/hàng

- Trường hợp 3 - justify-content: space-between, align-items: center (3 items)
  .container { display: flex; justify-content: space-between; align-items: center }
  ┌─────────────────────────────────┐
  │ Item1 Item2 Item3 │
  └─────────────────────────────────┘
  Item 1 bám trái, Item 3 bám phải, Item 2 ở giữa — tất cả căn giữa dọc theo cross axis

- Trường hợp 4 - grid-template-columns: 200px 1fr 200px (3 items)
  .container { display: grid; grid-template-columns: 200px 1fr 200px; gap: 20px }
  ┌─────────┬──────────────┬─────────┐
  │200px │ flex │ 200px │
  │ Item1 │ Item2 │ Item3 │
  └─────────┴──────────────┴─────────┘
  Sidebar cố định | nội dung co giãn | sidebar cố định. 1fr = tổng − 200 − 200 − 2×20gap

- Trường hợp 5 - repeat(3, 1fr), gap: 10px (7 items)
  .container { display: grid; grid-template-columns: repeat(3, 1fr); gap: 10px }
  ┌───────────┬───────────┬───────────┐
  │ Item1 │ Item2 │ Item3 │
  ├───────────┼───────────┼───────────┤
  │ Item4 │ Item5 │ Item6 │
  ├───────────┼───────────┼───────────┤
  │ Item7 │ │ │
  └───────────┴───────────┴───────────┘
  3 hàng, 3 cột. Item 7 ngồi ở cột 1 hàng 3 — 2 ô còn lại trống (grid không tự thu)

### Câu C1 — Flexbox vs Grid: Khi nào dùng gì?

1. Navigation bar ngang (logo + menu + buttons) -> Flexbox
   Giải thích: Nav bar là 1 chiều (các item xếp trên 1 hàng ngang). Flexbox sinh ra để làm việc này — dễ dàng đẩy logo sang trái, menu + buttons sang phải bằng margin-left: auto hoặc justify-content: space-between.
2. Lưới ảnh Instagram (3 cột đều nhau, số ảnh không biết trước) -> Grid
   Giải thích: Số ảnh không biết trước nhưng cấu trúc 2 chiều cố định (3 cột). Grid xử lý hoàn hảo — các item tự động xuống hàng đúng cột mà không cần tính toán.
3. Layout blog: main content + sidebar -> Grid
   Giải thích: Đây là bài toán 2 chiều có kích thước cụ thể — sidebar cố định, main co giãn. Grid cho phép định nghĩa đúng 1 lần, không cần hack.
4. Footer với 4 cột thông tin (Về chúng tôi, Liên kết, Hỗ trợ, Liên hệ) -> Flexbox hoặc Grid đều được
   Giải thích: Nếu 4 cột đều nhau, đơn giản → Flexbox với flex: 1 là đủ
   Nếu các cột có độ rộng khác nhau hoặc cần align phức tạp → Grid rõ ràng hơn
5. Card sản phẩm (ảnh trên, text giữa, nút dưới — nút luôn dính đáy) -> Flexbox
   Giải thích: Card là 1 chiều dọc (column). Trick "nút dính đáy" kinh điển: card dùng flex-direction: column, phần text giữa dùng flex: 1 để đẩy nút xuống đáy.

### Câu C2 — Debug Flexbox

Lỗi 1 — Nút "Mua" bị nhảy lên/xuống
Nguyên nhân: Card không có display: flex; flex-direction: column, nên chiều cao mỗi card co theo nội dung. Card nào title dài thì cao hơn → nút bị đẩy lên/xuống loạn.

Sửa:
.card {
width: 30%;
margin: 1.5%;
display: flex;
flex-direction: column; /_ xếp dọc _/
}

.card-body {
flex: 1; /_ ← phần text ăn hết khoảng trống _/
}

.card .btn {
padding: 10px;
margin-top: auto; /_ ← nút luôn dính đáy _/
}

Lỗi 2 — Item vẫn dính góc trái trên
Nguyên nhân: display: flex tạo ra flex container, nhưng thiếu 2 property căn giữa. Mặc định justify-content: flex-start (bám trái) và align-items: stretch (bám trên).

Sửa:

.hero {
height: 100vh;
display: flex;
justify-content: center; /_ căn giữa ngang (main axis) _/
align-items: center; /_ căn giữa dọc (cross axis) _/
}

/_ .hero-content không cần sửa _/

Lỗi 3 — Sidebar bị co lại
Nguyên nhân: Flexbox mặc định có flex-shrink: 1 — cho phép tất cả items co lại khi container thiếu chỗ. Khi .content có nhiều nội dung, flex tính toán lại và cũng co cả sidebar để cân bằng.

Sửa:

.sidebar {
width: 250px;
flex-shrink: 0; /_ ← không cho co _/
/_ hoặc viết gọn: flex: 0 0 250px; _/
}

.content {
flex: 1;
min-width: 0; /_ ← bonus: tránh content tràn ra ngoài _/
}
