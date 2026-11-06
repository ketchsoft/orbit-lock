# Sneaky Wipe: Tricky Reveal (PROTOTYPE - NOT FOR PRODUCTION)

Playable ad và bản test concept cho một game đố mẹo dạng "xoá để lộ cú lừa", thuộc dòng tricky riddle (Brain Out, Brain Test).

**Trạng thái:** in-progress

## Vì sao chọn game này

- Game tham chiếu: Brain Out (EYEWIND), đang #1 Word top free ở Việt Nam và #73 ở Mỹ, 4.6★ với 292k rating ở VN và 248k ở Mỹ. Ra năm 2019 mà gần như tháng nào cũng có bản cập nhật thêm màn. Dòng game này sống rất lâu.
- Điểm yếu của Brain Out: mỗi màn là một trò mẹo làm tay, chi phí nội dung cao. Bản của mình gom về **một cơ chế duy nhất** (xoá lớp phủ) để mỗi màn chỉ còn là dữ liệu: câu hỏi, 2 lớp ảnh và 1 vùng đích.
- Chỉ học cơ chế. Tên, art (vẽ bằng code), câu đố và màn chơi đều do mình làm, không sao chép game gốc.

## Giả thuyết

- **H1 (hiểu ngay):** người chơi hiểu cách chơi trong dưới 5 giây nhờ câu hỏi, bàn tay hướng dẫn và dòng "Wipe to find the truth!".
- **H2 (hook ads):** khoảnh khắc lộ cú lừa ("The CAT did it!"), cộng một lần đoán sai (con chó) và thanh tẩy sắp hết, đủ kéo CTR.
- **H3 (scale nội dung):** mỗi màn chỉ là cặp ảnh trước/sau và một mask, nên AI sinh ảnh làm được (fal.ai edit ảnh) cùng câu đố do Claude viết. Chi phí mỗi màn chỉ còn vài cent cộng thời gian người duyệt.

## Cơ chế

- Mỗi màn có một câu hỏi và một cảnh. Người chơi dùng ngón tay xoá lớp phủ để xem bên dưới.
- Thanh cục tẩy có giới hạn. Mỗi ô mới bị xoá tốn tẩy, nên xoá bừa sẽ hết tẩy và thua. Thắng khi lộ được 60% vùng đích.
- Có mồi đánh lạc hướng (con chó trông có lỗi, miếng phô mai) và manh mối nhỏ (đuôi mèo lòi ra khỏi rèm, vũng nước dưới người tuyết).
- Nút HINT nhấp nháy viền vùng đích (bản đầy đủ sẽ là rewarded ad). 3 màn, sau đó là end card PLAY FREE (`mraid.open` nếu có).
- Âm thanh tổng hợp bằng WebAudio, không dùng asset.

## Cách chạy

- Chơi: mở `index.html` trong trình duyệt (khổ dọc, chạy tốt ở 390px).
- `?demo=1`: tự chơi theo kịch bản, có caption ad. `?cap=1`: đồng hồ thủ công `window.__advance(dt)` để quay từng frame.
- Debug: `__game.state`, `__game.level(n)`, `__game.wipeTarget()`, `__events`.

## Link công khai

- Playable: https://ketchsoft.github.io/orbit-lock/sneaky-wipe/
- Video ad 23s: https://ketchsoft.github.io/orbit-lock/sneaky-wipe/ad-23s.mp4

Video và công cụ quay nằm ở `production/marketing/sneaky-wipe-ads/`.

## Đã kiểm tra (2026-11-06, Chromium headless)

- Chơi thật bằng thao tác kéo chuột ở viewport 390×844: qua cả 3 màn. Màn 3 cố tình xoá sai thì thua đúng ("Out of eraser!"). TRY AGAIN chơi lại được. PLAY FREE gọi `mraid.open` với link đúng (mraid giả). Không có lỗi JS.
- Bản demo của ad: màn 1 thắng ở 5,6s, màn 2 ở 10,3s, màn 3 ở 17,2s, end card ở 19,2s.
- **Chưa kiểm tra:** cảm giác xoá trên điện thoại thật, hiệu năng Android đời thấp, pipeline sinh màn bằng AI (mới là thiết kế).

## Kết quả

_(chờ test CPI)_
