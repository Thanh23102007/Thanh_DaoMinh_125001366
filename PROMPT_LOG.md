# NHẬT KÝ PROMPT ENGINEERING (VIBE CODING LOG)

- **Họ và tên:** Đào Minh Thanh
- **MSSV:** 125001366
- **Tên đề tài Website:** Giới thiệu đất nước Việt Nam
- **Công cụ AI đã sử dụng:** Antigravity (Google DeepMind) / Gemini 3.8 Flash

---

## 1. Yêu cầu ban đầu (System/Initial Prompt)

*(Ghi chú: Sinh viên gửi chuỗi 3 prompt ban đầu cùng lúc để AI xây dựng nền tảng và nhận bản code đầu tiên)*

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
  - Khởi tạo đầy đủ 2 file `index.html` và `style.css` với cấu trúc HTML5 ngữ nghĩa (`<header>`, `<nav>`, `<main>`, `<section>`, `<article>`, `<figure>`, `<footer>`).
  - Đầy đủ 4 section nội dung: Giới thiệu chung, Ba miền, Ẩm thực, Địa danh nổi tiếng với tone màu đỏ - vàng đặc trưng.
  - Tích hợp thành công hiệu ứng Animate.css cho tiêu đề và nút bấm ở Header; gắn `data-aos="fade-up"` cho các section kèm khởi tạo `AOS.init()` ở cuối `<body>`.
  - Dàn bố cục kết hợp Flexbox cho thanh điều hướng và CSS Grid cho lưới card thông tin, đồng thời tối ưu responsive cho di động.
- **Nhận xét & Tinh chỉnh của SV:**
  - Code được tạo nhanh chóng, tuy nhiên cần đồng bộ trực tiếp vào VS Code đang mở và kiểm thử chi tiết về mặt tương tác bàn phím, chuẩn code và tính tiện dụng khi cuộn trang.
- **Thách thức gặp phải / Cách sửa prompt (Debug prompt):**
  - Môi trường thực tế mở ở thư mục khác (`C:\Users\LHUser\Downloads\125001366_ĐàoMinhThanh`), đã dùng prompt yêu cầu AI dán thẳng code vào VS Code để cập nhật trực tiếp vào dự án.

---

### Lần 2: Sửa lỗi thẻ Card không nhận hiệu ứng :focus khi bấm phím Tab
- **Prompt đã dùng:**  
  `Trong style.css, các card không nhận hiệu ứng :focus khi mình bấm phím Tab. Hãy thêm tabindex="0" cho các thẻ article.info-card trong index.html và giữ nguyên CSS focus hiện có. Chỉ sửa đúng chỗ đó.`
- **Kết quả AI tạo ra:**
  - Thêm thuộc tính `tabindex="0"` vào 10 thẻ `<article class="info-card">` (3 card Ba Miền, 4 card Món Ăn, 3 card Địa Danh) trong file `index.html`.
  - Giữ nguyên toàn bộ cấu trúc CSS focus hiện có trong `style.css`.
- **Nhận xét & Tinh chỉnh của SV:**
  - Khi sử dụng phím `Tab` trên bàn phím, con trỏ duyệt qua lần lượt từng card, kích hoạt đúng hiệu ứng `:focus` và `:focus-visible` (card nổi lên 8px, đổi đường viền sang màu vàng và tăng bóng đổ).
- **Thách thức gặp phải / Cách sửa prompt (Debug prompt):**
  - *Nguyên nhân:* Thẻ `<article>` không phải là phần tử tương tác mặc định (interactive element như `<button>`, `<a>`, `<input>`) nên trình duyệt bỏ qua khi duyệt phím Tab.
  - *Giải pháp:* Prompt chỉ định bổ sung `tabindex="0"` trực tiếp vào các thẻ `<article.info-card>` để đưa card vào luồng Tab index tự nhiên mà không cần dùng JavaScript.

---

### Lần 3: Sửa lỗi thiếu biến CSS Spacing / Cỡ chữ, dọn dẹp mã màu ghi cứng và biến không dùng
- **Prompt đã dùng:**  
  `Trong style.css, hãy thêm CSS variables cho spacing (--space-sm, --space-md, --space-lg) và cỡ chữ, thay các màu ghi cứng như #ffffff, #1a1a1a bằng biến, và xóa các biến không dùng. Không làm đổi giao diện.`
- **Kết quả AI tạo ra:**
  - Bổ sung hệ thống biến khoảng cách Spacing: `--space-xs`, `--space-sm`, `--space-md`, `--space-lg`, `--space-xl`, `--space-2xl`.
  - Bổ sung hệ thống biến cỡ chữ Typography: `--font-xs`, `--font-sm`, `--font-base`, `--font-md`, `--font-lg`, `--font-xl`, `--font-2xl`.
  - Thay thế 100% các mã màu hex ghi cứng bên ngoài `:root` (như `#ffffff`, `#1a1a1a`, `#333333`, `#d1d1d1`, `#888888`, `#000000`,...) thành các biến `var(...)`.
  - Loại bỏ hoàn toàn 4 biến rác khai báo nhưng không dùng: `--secondary-dark`, `--bg-alt`, `--radius-lg`, `--shadow-md`.
- **Nhận xét & Tinh chỉnh của SV:**
  - File `style.css` được chuẩn hóa theo chuẩn "Clean Code", toàn bộ màu sắc, khoảng cách và cỡ chữ đều quản lý tập trung tại `:root`, giao diện hiển thị được giữ nguyên 100%.
- **Thách thức gặp phải / Cách sửa prompt (Debug prompt):**
  - *Nguyên nhân:* Phiên bản ban đầu còn sót các giá trị màu và khoảng cách ghi cứng trực tiếp trong các class.
  - *Giải pháp:* Ra lệnh cụ thể cho AI bổ sung các biến chuẩn hóa, thay thế triệt để các mã màu cứng và rà soát xóa các biến không sử dụng mà không làm xê dịch giao diện.

---

### Lần 4: Tinh chỉnh Header, Menu Sticky cố định trên cùng, tách Banner ra Main và chống che khuất tiêu đề
- **Prompt đã dùng:**  
  `Mình muốn sửa phần đầu trang trong index.html và style.css:
  1. Xóa hoàn toàn thẻ <span class="flag-icon">🇻🇳</span> ở logo, và xóa luôn CSS .flag-icon trong style.css. Chỉ giữ lại chữ "Việt Nam Quê Hương Tôi".
  2. Làm cho thanh menu (logo + Giới thiệu, Ba miền, Ẩm thực, Địa danh) luôn dính ở trên cùng khi cuộn trang:
  - Hiện tại banner (section.hero-banner) đang nằm trong <header>. Hãy chuyển banner ra ngoài <header>, đặt ngay đầu <main> và giữ nguyên nội dung, class và hiệu ứng Animate.css của nó.
  - Cho .site-header dùng position: sticky; top: 0; z-index: 1000; giữ nguyên nền gradient đỏ và đổ bóng.
  - Vì banner không còn nằm trong header nên hãy cho .hero-banner nền gradient đỏ như cũ và để banner trải rộng hết chiều ngang màn hình.
  - Thêm scroll-margin-top cho các section (#gioi-thieu, #ba-mien, #am-thuc, #dia-danh) để khi bấm menu, tiêu đề section không bị thanh menu che.
  Chỉ sửa những chỗ cần thiết, giữ nguyên các phần còn lại. Sau khi sửa, cho mình biết bạn đã đổi những gì.`
- **Kết quả AI tạo ra:**
  - Xóa bỏ icon cờ `🇻🇳` ở logo trong cả `index.html` và xóa class `.flag-icon` trong `style.css`.
  - Di chuyển `section.hero-banner` ra khỏi `<header>` và đặt ngay đầu `<main>`, thiết lập `width: 100%` với nền gradient đỏ trải rộng toàn màn hình.
  - Thiết lập `.site-header` dính trên cùng với `position: sticky; top: 0; z-index: 1000;`.
  - Thêm thuộc tính `scroll-margin-top: 80px;` cho các section (`#gioi-thieu`, `#ba-mien`, `#am-thuc`, `#dia-danh`).
- **Nhận xét & Tinh chỉnh của SV:**
  - Thanh menu giờ đây luôn bám cố định ở mép trên màn hình khi cuộn trang.
  - Khi người dùng bấm vào các liên kết menu, trang web cuộn mượt mà và dừng lại chính xác bên dưới thanh menu dính, hoàn toàn không bị menu che khuất tiêu đề section.
- **Thách thức gặp phải / Cách sửa prompt (Debug prompt):**
  - *Nguyên nhân:* Trước đó hero-banner nằm chung trong `<header>` nên không thể làm sticky riêng thanh điều hướng; khi menu sticky xuất hiện sẽ che khuất phần đầu của các section khi bấm anchor link.
  - *Giải pháp:* Tách cấu trúc rõ ràng (thanh menu thuộc `<header>`, banner chuyển vào `<main>`) và áp dụng giải pháp chuẩn CSS `scroll-margin-top` tương ứng với chiều cao của menu sticky.

---

### Danh sách các điểm rà soát khác (nếu có):
- Footer thiếu thông tin liên hệ chi tiết: (SV tự bổ sung nếu cần mở rộng)
- Thay đổi link CDN thư viện khi triển khai thực tế: (SV tự bổ sung nếu cần)

---

## 3. Đánh giá cá nhân về quá trình Vibe Coding

### AI giúp mình tiết kiệm thời gian ở phần nào nhất?
1. **Khởi tạo mã nguồn và nội dung mẫu:** AI giúp tạo toàn bộ khung HTML ngữ nghĩa chuẩn và đoạn văn giới thiệu Việt Nam chân thực, giàu cảm xúc mà không cần mất công gõ tay từng dòng.
2. **Xây dựng hệ thống layout CSS phức tạp:** Thiết lập nhanh chóng CSS Grid tự động chia cột (`repeat(auto-fit, minmax(...))`), Flexbox và bảng biến CSS Variables.
3. **Responsive Design và Xử lý sự cố tương tác:** Căn chỉnh media query cho nhiều kích thước màn hình và xử lý các lỗi CSS nâng cao như `scroll-margin-top` hay tính tiếp cận `tabindex`.

### Bài học rút ra khi đặt prompt cho AI trong thiết kế web?
1. **Chia nhỏ yêu cầu và lặp từng bước (Iterative Prompting):** Không nên nhồi nhét tất cả vào một lần nếu chưa chắc chắn; việc kiểm thử từng tính năng và prompt tinh chỉnh từng bước giúp kiểm soát chất lượng code chặt chẽ.
2. **Mô tả cụ thể cả "triệu chứng" lẫn "giải pháp mong muốn":** Khi gặp lỗi (ví dụ card không nhận focus hay menu che tiêu đề), mô tả rõ ràng hành vi lỗi và yêu cầu thuộc tính kỹ thuật cụ thể (`tabindex="0"`, `scroll-margin-top`) giúp AI sửa đúng mục tiêu mà không làm ảnh hưởng phần khác.
3. **Luôn yêu cầu "Chỉ sửa chỗ cần thiết, giữ nguyên phần còn lại":** Đây là nguyên tắc cốt lõi trong Vibe Coding để tránh tình trạng AI tự ý viết lại hoặc làm mất các đoạn code đã hoạt động tốt trước đó.
