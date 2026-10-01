# Spec Delta

## Purpose

Cho phép người chơi khám phá một kỹ năng tự chọn qua nhiệm vụ phụ ngắn, trong khi vòng Main Mission vẫn trọn vẹn nếu họ chưa muốn học kỹ năng.

## ADDED Requirements

### Requirement: Người chơi chọn kỹ năng
Prototype SHALL đưa vài gợi ý kỹ năng khác nhau và cho phép chọn một kỹ năng hoặc chưa chọn; SHALL không tự động biến gợi ý thành cam kết.

#### Scenario: Chưa muốn chọn
- **WHEN** người chơi bỏ qua danh sách kỹ năng
- **THEN** họ vẫn hoàn tất vòng Main Mission mà không bị nhắc như đang thiếu nhiệm vụ

#### Scenario: Chọn kỹ năng
- **WHEN** người chơi chọn một gợi ý
- **THEN** prototype ghi kỹ năng đó là hướng khám phá hiện tại và cho phép đổi về sau

### Requirement: Growth Mission thật sự tùy chọn
Prototype SHALL chỉ trình bày Growth Mission như lựa chọn thêm và cho phép bỏ qua, đổi hoặc tạm dừng mà không tạo việc tồn đọng.

#### Scenario: Ngày ít sức
- **WHEN** người chơi không còn sức hoặc không mở nhiệm vụ kỹ năng
- **THEN** prototype không bắt hoàn thành Growth Mission và vẫn cho kết thúc ngày

#### Scenario: Muốn đổi kỹ năng
- **WHEN** người chơi yêu cầu đổi hướng khám phá
- **THEN** prototype cho phép chọn lại, không xem kỹ năng cũ là thất bại
