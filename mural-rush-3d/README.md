# Mural Rush 3D: Paint Bots (PROTOTYPE - NOT FOR PRODUCTION)

Biến thể B của Mural Rush cho đợt test CPI: **cùng cơ chế, cùng 3 bức tranh, chỉ đổi phần hình sang 3D** (tranh voxel, robot đồ chơi 3D). Mục đích là so A/B với bản 2D (`../mural-rush/`) để biết 3D có kéo CTR, IPM tốt hơn không.

**Trạng thái:** in-progress

## Vì sao làm bản 3D

- Bản 2D trông gần dòng Pixel Flow, nên dễ bị xem là hàng na ná và quảng cáo đắt. Bản 3D có cảnh "tranh mọc lên thành khối" khác hẳn.
- Thị trường quen tên "3D" ở dòng puzzle thú, khối (ví dụ subtitle "3D Farm Parking Game" của Sheep Jam, Sheep Sort: 3D Color Puzzle).
- Robot đồ chơi 3D dễ thương hợp với đối tượng nữ 25 đến 55 tuổi hơn robot phẳng.
- Chỉ học cơ chế. Tên, robot, hệ Dock, tranh và thuật toán sinh màn đều là của mình.

## Giả thuyết

- **H1 (A/B):** creative 3D có CTR hoặc IPM cao hơn bản 2D ít nhất 20% với cùng ngân sách. Nếu ngang nhau thì giữ 2D vì nhẹ và rẻ hơn.
- **H2 (dễ đọc):** góc camera nghiêng vẫn cho thấy rõ hàng, cột và luật "lớp ngoài trước".
- **H3 (hiệu năng):** 144 voxel + 5 robot + hạt chạy mượt trên Android tầm thấp (chưa đo).

## Khác với bản 2D

- Logic (băng chuyền, bắn ô đầu tiên của hàng hay cột, Dock 5 chỗ, sinh màn bằng bóc lớp) giữ nguyên.
- Hình: Three.js r160. Ô chưa tô là khối thấp màu kem có chấm màu, tô xong khối nảy cao lên (back-ease). Thắng: sóng khối lan từ tâm, bàn xoay nhẹ cho thấy chiều sâu. End card: tranh 3D xoay, 5 robot nhảy.
- Băng chuyền có thanh trượt chạy thật, robot quay mặt theo hướng chạy, bắn đạn sơn theo đường cong.
- HUD (tiêu đề, %, caption, ngón tay, nút) vẽ trên canvas 2D đè lên WebGL.
- Bản ad: nửa cuối màn tăng tốc băng chuyền 1,6 lần để tranh xong ở 15,3s (bản 2D: 14,3s), end card từ 20s.

## Cách chạy

`index.html` là bản build một file (three.min.js đã inline, khoảng 690 KB, không gọi mạng ngoài). Mạng quảng cáo yêu cầu điều này. Sửa code ở `game.src.html` rồi build lại:

```bash
npm i three@0.160.0            # trong thư mục tạm bất kỳ
node build.js /path/to/node_modules/three/build/three.min.js
```

- Chơi: mở `index.html` (khổ dọc, chạy tốt ở 390px).
- Ad chạy lặp 23s: `index.html?ad=1` (hoặc `?demo=1`).
- Quay từng frame: `index.html?ad=1&rec=1` (hoặc `?cap=1`), gọi `window.__adStep(1/30)` (alias `__advance`).
- Debug: `__game.state`, `__game.level(n)`, `__bestTap()` (toạ độ CSS của robot nên bấm), `__events`.
- Nút PLAY FREE gọi `mraid.open()` khi có MRAID.

## Link công khai

- Playable: https://ketchsoft.github.io/orbit-lock/mural-rush-3d/
- Ad chạy lặp: https://ketchsoft.github.io/orbit-lock/mural-rush-3d/?ad=1
- Video ad 23s: https://ketchsoft.github.io/orbit-lock/mural-rush-3d/ad-23s.mp4

Video và công cụ quay: `production/marketing/mural-rush-3d-ads/`.

## Đã kiểm tra (2026-11-08, Chrome for Testing headless, WebGL phần mềm)

- Chơi đủ 3 màn bằng click thật ở viewport 390×844: Strawberry 57/57, Ginger Cat 112/112, Moon Rocket 68/68, rồi tới end card. Không có lỗi JS.
- Mô phỏng ad: tranh xong ở 15,3s, Dock dùng tối đa 1/5, không lỗi.
- Ảnh: `screenshots/` (hướng dẫn màn 1, thắng màn 1, thắng màn 3, end card, dải frame của ad).
- **Chưa kiểm tra:** cảm giác bấm trên điện thoại thật (bấm trúng robot nhờ raycast và vùng dự phòng 70px), fps trên Android tầm thấp, màn thua (Dock đầy) chưa được ép ra trong test tự động.

## Kết quả

_(chờ test CPI, so với bản 2D)_
