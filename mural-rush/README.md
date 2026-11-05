# Mural Rush: Paint Bots (PROTOTYPE - NOT FOR PRODUCTION)

Playable ad và bản test concept cho một game puzzle hybrid-casual thuộc dòng conveyor bắn màu.

**Trạng thái:** in-progress

## Vì sao chọn game này

- Tín hiệu thị trường: Pixel Flow (dòng conveyor bắn màu) đạt hơn 125 triệu USD IAP trong chưa đầy 1 năm (AppMagic H1 2026), Scopely mua đa số cổ phần. Hybrid-casual tăng 23% IAP ở H1 2026 (Sensor Tower).
- Chỉ nghiên cứu cơ chế, sản phẩm là của mình: tên, robot sơn (vẽ bằng code), hệ Dock, bộ tranh pixel và thuật toán sinh màn đều tự làm. Không sao chép tên, nhân vật hay art của game gốc.

## Giả thuyết

- **H1 (hiểu ngay):** người chơi hiểu luật trong dưới 5 giây nhờ bàn tay hướng dẫn và câu "Tap a bot to send it out!".
- **H2 (hook ads):** cảnh bức tranh pixel đầy dần lên, kèm áp lực Dock đầy, đủ hấp dẫn để có CTR tốt.
- **H3 (scale nội dung):** sinh màn tự động từ ảnh pixel bất kỳ và luôn giải được, nên chi phí làm thêm màn gần như bằng 0.

## Cơ chế

- Bức tranh pixel bị phai màu; mỗi ô có chấm màu chỉ màu cần tô.
- Bấm robot ở hàng chờ (3 cột) để thả lên băng chuyền (tối đa 5 robot). Robot chạy một vòng quanh tranh. Đi tới hàng hay cột nào, nó bắn vào ô chưa tô đầu tiên của hàng hay cột đó nếu ô cùng màu với nó. Số trên thân là lượng sơn còn lại.
- Hết sơn thì robot biến mất. Hết vòng mà còn sơn thì robot vào Dock 5 chỗ; bấm robot trong Dock để thả lại. Dock đầy là thua.
- Sinh màn: bóc lớp tranh từ ngoài vào, chia mỗi màu thành các robot khoảng 10 sơn, xếp robot của lớp ngoài lên trước.
- 3 màn: Strawberry (9×9), Ginger Cat (12×12), Moon Rocket (12×12), sau đó là end card PLAY FREE.
- Âm thanh tổng hợp bằng WebAudio, không dùng asset.

## Cách chạy

- Chơi: mở `index.html` trong trình duyệt (khổ dọc, chạy tốt ở 390px).
- Bản ad chạy lặp 23s: `index.html?ad=1`.
- Chế độ render từng frame cho recorder: `index.html?ad=1&rec=1` (gọi `window.__adStep(1/30)` để tiến 1 frame).

## Link công khai

- Playable: https://ketchsoft.github.io/orbit-lock/mural-rush/
- Bản ad chạy lặp: https://ketchsoft.github.io/orbit-lock/mural-rush/?ad=1
- Video ad 23s: https://ketchsoft.github.io/orbit-lock/mural-rush/ad-23s.mp4

## Video ad và hồ sơ

Nằm ở `production/marketing/mural-rush-ads/`:

- `mural-rush-ad-23s.mp4`: 9:16, 1080×1920, 23,0s, có âm thanh. Hook 0 đến 2,6s, tranh xong ở 14,3s, end card từ 20s.
- `SUBMISSION.md`: hồ sơ Launchpad gate G1 → G2 (Test CPI), ngân sách 1.074 USD.
- `tools/`: script Node + Playwright để mô phỏng, render frame, tổng hợp âm thanh và test chơi thật (xem README trong thư mục đó).

## Đã kiểm tra

- Mô phỏng bản ad: hoàn thành tranh ở 14,3s, Dock đầy tối đa 1/5, không có lỗi JS.
- Chơi đủ 3 màn bằng click thật ở viewport 390×844, không có lỗi JS.
- Nút PLAY FREE gọi `mraid.open()` khi có MRAID (đã test bằng mraid giả, 2026-11-05).
- **Chưa kiểm tra:** cảm giác trên điện thoại thật, hiệu năng Android đời thấp.

## Kết quả

_(chờ test CPI)_
