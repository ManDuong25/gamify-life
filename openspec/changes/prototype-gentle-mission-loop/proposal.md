# Proposal

## Why

Vòng chơi hiện mới là giả thuyết: nhận một nhiệm vụ rồi đánh dấu hoàn tất có thể hữu ích nhưng chưa chắc tạo cảm giác game. Cần một prototype ngắn để thử quyền chọn, giá trị hành động ngoài đời và cảm giác tiếp nối của hành trình hồi phục, khám phá trước khi chọn công nghệ hoặc xây hệ thống AI.

## What Changes

- Đề xuất prototype tương tác thấp cho một vòng ngày: nắm bối cảnh tối thiểu, đưa một Main Mission, cho người chơi nhận/sửa/giảm/hoãn/từ chối, ghi nhận kết quả và dùng lựa chọn đó cho lượt sau.
- Chỉ hiện nhánh chọn ưu tiên khi có xung đột thật giữa hai việc người chơi đã xác nhận; không tự ép ưu tiên sức khỏe hay hạn chót.
- Thử phản hồi “dấu vết hành trình” thể hiện điều đã thử, điều muốn giữ hoặc đổi, không dùng XP, streak hay điểm sức khỏe.
- Thử một hành trình kỹ năng tùy chọn bằng gợi ý được biên soạn trước; không cần AI trực tiếp để chơi prototype.
- Ghi tiêu chí playtest và quyết định đi tiếp, sửa hay dừng trước vertical slice. Đây là đề xuất để duyệt, chưa phải tính năng đã xây hoặc hiệu quả đã được chứng minh.

## Capabilities

### New Capabilities

- `daily-mission-loop`: Luồng chọn, điều chỉnh, phản hồi Main Mission và nhánh xung đột ưu tiên trong prototype.
- `optional-skill-journey`: Việc chọn một kỹ năng để khám phá và nhiệm vụ phụ hoàn toàn tùy chọn trong prototype.

### Modified Capabilities

- Không có; kho đặc tả hiện hành chưa có capability game.

## Impact

- Tạo prototype và kịch bản playtest; chưa chọn nền tảng sản phẩm, nhà cung cấp AI, tài khoản, cơ chế điểm thưởng hoặc kiến trúc lưu dữ liệu dài hạn.
- Phạm vi an toàn: không chẩn đoán, điều trị, suy luận khả năng vận động từ triệu chứng hoặc khẳng định một hoạt động phù hợp khi thiếu dữ kiện.
- Kết quả playtest có thể yêu cầu sửa hoặc bác bỏ vòng chơi; không tự động chuyển sang vertical slice.
