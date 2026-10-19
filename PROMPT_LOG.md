# NHẬT KÝ PROMPT ENGINEERING (VIBE CODING LOG)

- **Họ và tên:** Đào Minh Thanh
- **MSSV:** 125001366
- **Tên đề tài Website:** Giới thiệu đất nước Việt Nam
- **Công cụ AI đã sử dụng:** Antigravity (Google DeepMind) / Gemini 3.8 Flash

---

## 1. Yêu cầu ban đầu (System/Initial Prompt)

*(Ghi chú: Sinh viên gửi chuỗi 3 prompt yêu cầu ban đầu để xây dựng cấu trúc nền tảng và nhận bản code đầu tiên)*

### Prompt ban đầu 1 (Dựng khung HTML/CSS ngữ nghĩa):
> "Mình là sinh viên mới học web. Hãy giúp mình làm một trang web đơn giản giới thiệu đất nước Việt Nam bằng 2 file: index.html và style.css.
> 
> Yêu cầu:
> - Dùng các thẻ HTML ngữ nghĩa: header, nav, main, section, footer (hạn chế dùng div).
> - Trang có 4 phần: Giới thiệu chung, Ba miền, Ẩm thực, Địa danh nổi tiếng.
> - Trong style.css, khai báo màu và font ở :root bằng CSS variables (ví dụ --primary-color), rồi dùng lại các biến đó.
> - Dùng Flexbox hoặc Grid để xếp các thẻ nội dung (card).
> - Màu chủ đạo đỏ và vàng.
> - Viết comment tiếng Việt giải thích từng phần, và đừng viết JavaScript."

### Prompt ban đầu 2 (Tích hợp thư viện hiệu ứng Animate.css và AOS):
> "Được rồi làm tiếp nè Bây giờ hãy thêm vào trang này:
> - Thư viện Animate.css (link CDN) cho tiêu đề và nút ở phần đầu trang.
> - Thư viện AOS (link CDN) cho các section khi cuộn trang. Nhớ nhúng file aos.js và gọi AOS.init() ở cuối body.
> Chỉ sửa những chỗ cần thiết, giữ nguyên phần còn lại. Giải thích ngắn gọn bạn đã thêm gì."

### Prompt ban đầu 3 (Thêm hiệu ứng tương tác Hover/Focus và Responsive Mobile):
> "Được rồi làm tiếp nè Hãy thêm hiệu ứng :hover và :focus cho nút bấm và các card (đổi màu hoặc nổi lên nhẹ). Sau đó làm cho trang hiển thị tốt trên điện thoại bằng media query. Chỉ sửa file style.css."

---

## 2. Quá trình tinh chỉnh & Giải quyết sự cố (Iteration)

### Lần 1: Dựng khung và nhận kết quả đầu tiên
- **Prompt đã dùng:** Tập hợp 3 prompt ban đầu ở mục 1, kết hợp prompt hỗ trợ đồng bộ:  
  `t muốn bạn dán thẳng code vào vs studio code mà t đang mở`
- **Kết quả AI tạo ra:**
  - Tạo thành công 2 file `index.html` và `style.css` chuẩn HTML5 ngữ nghĩa (`<header>`, `<nav>`, `<main>`, `<section>`, `<article>`, `<figure>`, `<footer>`).
  - Giao diện có 4 section hoàn chỉnh: Giới thiệu chung, Ba miền, Ẩm thực, Địa danh nổi tiếng với tone màu đỏ - vàng.
  - Tích hợp hiệu ứng xuất hiện Animate.css cho tiêu đề và nút bấm, hiệu ứng cuộn trang AOS `data-aos="fade-up"` cho các section.
  - Bố cục sử dụng Flexbox cho Navbar/Hero và CSS Grid cho hệ thống Card.
- **Nhận xét & Tinh chỉnh của SV:**
  - AI sinh code rất nhanh và đúng cấu trúc, tuy nhiên cần kiểm tra kỹ tính tương tác thực tế khi thao tác trực tiếp trên trình duyệt và phím bấm.
- **Thách thức gặp phải / Cách sửa prompt (Debug prompt):**
  - Môi trường làm việc mở ở thư mục khác, đã dùng prompt yêu cầu AI dán thẳng code vào VS Code đang mở để đồng bộ hóa mã nguồn tức thì.

---

### Lần 2: Sửa lỗi thẻ Card không nhận hiệu ứng :focus khi bấm phím Tab
- **Prompt đã dùng:**  
  `Trong style.css, các card không nhận hiệu ứng :focus khi mình bấm phím Tab. Hãy thêm tabindex="0" cho các thẻ article.info-card trong index.html và giữ nguyên CSS focus hiện có. Chỉ sửa đúng chỗ đó.`
- **Kết quả AI tạo ra:**
  - Bổ sung thuộc tính `tabindex="0"` vào toàn bộ 10 thẻ `<article class="info-card">` (3 card Ba Miền, 4 card Món Ăn, 3 card Địa Danh) trong `index.html`.
  - Giữ nguyên cấu trúc CSS và các thẻ HTML khác.
- **Nhận xét & Tinh chỉnh của SV:**
  - Sau khi thêm `tabindex="0"`, khi bấm phím `Tab` trên bàn phím, con trỏ duyệt qua lần lượt từng card, kích hoạt đúng trạng thái `:focus` và `:focus-visible` (card nổi lên 8px, viền chuyển vàng và đổ bóng).
- **Thách thức gặp phải / Cách sửa prompt (Debug prompt):**
  - *Nguyên nhân:* Thẻ `<article>` không phải là phần tử tương tác mặc định (interactive element như `<button>`, `<a>`, `<input>`) nên trình duyệt bỏ qua trong luồng duyệt phím Tab.
  - *Giải pháp:* Prompt chỉ thị cụ thể thêm `tabindex="0"` vào thẻ `<article.info-card>` để đưa card vào luồng điều hướng tuần tự của bàn phím mà không cần can thiệp JavaScript.

---

### Lần 3: Sửa lỗi thiếu biến CSS Spacing / Cỡ chữ, dọn dẹp mã màu ghi cứng và biến không dùng
- **Prompt đã dùng:**  
  `Trong style.css, hãy thêm CSS variables cho spacing (--space-sm, --space-md, --space-lg) và cỡ chữ, thay các màu ghi cứng như #ffffff, #1a1a1a bằng biến, và xóa các biến không dùng. Không làm đổi giao diện.`
- **Kết quả AI tạo ra:**
  - Khai báo bổ sung trong `:root` các biến khoảng cách: `--space-xs`, `--space-sm`, `--space-md`, `--space-lg`, `--space-xl`, `--space-2xl`.
  - Khai báo hệ thống biến cỡ chữ: `--font-xs`, `--font-sm`, `--font-base`, `--font-md`, `--font-lg`, `--font-xl`, `--font-2xl`.
  - Thay thế toàn bộ mã màu hex ghi cứng bên ngoài `:root` (như `#ffffff`, `#1a1a1a`, `#333333`, `#d1d1d1`, `#888888`, `#000000`,...) thành các biến `var(...)`.
  - Loại bỏ hoàn toàn 4 biến rác không sử dụng: `--secondary-dark`, `--bg-alt`, `--radius-lg`, `--shadow-md`.
- **Nhận xét & Tinh chỉnh của SV:**
  - File `style.css` trở nên sạch đẹp (clean code), chuẩn kiến trúc CSS Variables hiện đại, dễ dàng tùy biến giao diện mà không làm thay đổi dù chỉ 1 pixel hiển thị thực tế.
- **Thách thức gặp phải / Cách sửa prompt (Debug prompt):**
  - *Nguyên nhân:* Phiên bản ban đầu còn sót các màu ghi cứng rải rác trong file và một số biến khai báo sẵn từ đầu nhưng không dùng đến.
  - *Giải pháp:* Ra lệnh cụ thể cho AI bổ sung các biến chuẩn hóa khoảng cách và cỡ chữ, đồng thời rà soát xóa triệt để biến thừa và đưa 100% màu sắc về biến toàn cục.

---

### Danh sách các điểm rà soát khác (nếu có):
- Footer thiếu liên hệ chi tiết: (SV tự bổ sung nếu cần mở rộng)
- Thay đổi CDN thư viện khi triển khai production: (SV tự bổ sung nếu cần)

---

## 3. Đánh giá cá nhân về quá trình Vibe Coding

### AI giúp mình tiết kiệm thời gian ở phần nào nhất?
1. **Viết khung HTML và nội dung mẫu:** AI giúp tạo lập cực nhanh toàn bộ cấu trúc ngữ nghĩa HTML5 đầy đủ kèm văn bản mô tả giới thiệu Việt Nam chân thực, giàu cảm xúc mà không cần mất công soạn thủ công.
2. **Thiết lập layout CSS hiện đại:** AI tạo chuẩn xác hệ thống CSS Grid tự động co giãn (`repeat(auto-fit, minmax(...))`) và Flexbox, kết hợp các hiệu ứng hover, focus, animation mượt mà.
3. **Responsive Design:** Tiết kiệm hàng giờ viết và căn chỉnh `@media query` cho màn hình điện thoại và máy tính bảng.

### Bài học rút ra khi đặt prompt cho AI trong thiết kế web?
1. **Yêu cầu càng chi tiết, kết quả càng chuẩn xác:** Khi nêu rõ ràng các thẻ HTML ngữ nghĩa cần dùng, bảng màu chủ đạo và cấu trúc từng phần, AI sẽ không tạo code chung chung hay lạm dụng thẻ `<div>`.
2. **Quy tắc "Chỉ sửa chỗ cần thiết":** Trong các lần tinh chỉnh tiếp theo (Iteration), luôn yêu cầu AI chỉ can thiệp vào đúng phần cần sửa để tránh làm xáo trộn hoặc mất các tính năng đã làm tốt trước đó.
3. **Kết hợp kiểm thử thực tế và Debug bằng Prompt:** AI có thể tạo giao diện đẹp mắt nhưng có thể thiếu sót về tính tiếp cận (Accessibility như `tabindex` cho phím Tab). Việc trực tiếp trải nghiệm, phát hiện vấn đề và mô tả chính xác triệu chứng giúp AI đưa ra giải pháp sửa lỗi nhanh chóng và tối ưu nhất.
