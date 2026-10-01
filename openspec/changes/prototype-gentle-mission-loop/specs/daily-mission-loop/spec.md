# Spec Delta

## Purpose

Cho phép thử một vòng chơi ngày ngắn, trong đó người chơi tự quyết định một hành động đời thật, phản hồi về nó và nhìn thấy lựa chọn của mình ảnh hưởng lượt tiếp theo.

## ADDED Requirements

### Requirement: Hỏi đúng dữ kiện cần thiết
Prototype SHALL dùng bối cảnh còn phù hợp và chỉ hỏi thêm dữ kiện có thể làm thay đổi mission; người chơi SHALL được bỏ qua câu hỏi.

#### Scenario: Đã đủ bối cảnh
- **WHEN** ưu tiên, quỹ thời gian và giới hạn liên quan đã rõ và còn phù hợp
- **THEN** prototype đưa đề xuất mà không lặp lại bảng hỏi

#### Scenario: Thiếu dữ kiện quan trọng
- **WHEN** thiếu một dữ kiện có thể đổi đề xuất và người chơi chọn bỏ qua
- **THEN** prototype không giả định dữ kiện đó là đã biết và vẫn cho phép tự chọn một hành động phù hợp

### Requirement: Một Main Mission có thể lựa chọn
Prototype SHALL trình bày tối đa một Main Mission chính tại một thời điểm, kèm bước bắt đầu, dấu hiệu hoàn tất và lý do đề xuất ngắn.

#### Scenario: Nhận mission
- **WHEN** người chơi xem thẻ mission phù hợp với bối cảnh đã xác nhận
- **THEN** họ thấy hành động cụ thể, cách biết đã làm xong và tùy chọn nhận hoặc thay đổi

### Requirement: Người chơi kiểm soát mission
Prototype SHALL cho phép nhận hoặc mở lựa chọn điều chỉnh/bỏ qua; từ nhóm thứ hai người chơi SHALL đến được thao tác giảm tải, thay, tự đặt, hoãn hoặc từ chối mà không phạt hay tự diễn giải lựa chọn đó là thất bại. Prototype SHALL không buộc hiển thị mọi thao tác cùng lúc.

#### Scenario: Mission quá sức
- **WHEN** người chơi chọn giảm tải hoặc thay mission
- **THEN** prototype hiển thị một lựa chọn nhẹ hơn hoặc cho người chơi tự ghi hành động phù hợp trước khi xác nhận

#### Scenario: Từ chối mission
- **WHEN** người chơi từ chối hoặc hoãn
- **THEN** vòng chơi kết thúc bình thường, không tạo khoản phải bù hay giảm điểm

### Requirement: Xung đột ưu tiên có điều kiện
Prototype SHALL chỉ hỏi người chơi chọn hướng ưu tiên khi có hai mục tiêu cạnh tranh được họ xác nhận; lựa chọn của họ SHALL quyết định mission tiếp theo trong lượt đó.

#### Scenario: Có hạn chót thật cạnh tranh với hồi phục
- **WHEN** người chơi xác nhận một hạn chót cần xử lý, một ưu tiên khác họ vẫn muốn bảo vệ và hai hướng thực sự cạnh tranh trong quỹ sức hoặc thời gian hiện có
- **THEN** prototype nêu ngắn đánh đổi, cho chọn hướng ưu tiên, rồi đưa mission tương ứng với hướng đã chọn

#### Scenario: Không có xung đột
- **WHEN** không có hai ưu tiên cạnh tranh đã xác nhận
- **THEN** prototype bỏ qua màn chọn hướng ưu tiên

#### Scenario: Có deadline nhưng không xung đột
- **WHEN** người chơi có deadline nhưng vẫn đủ chỗ cho ưu tiên khác hoặc không xác nhận có đánh đổi
- **THEN** prototype bỏ qua màn chọn hướng ưu tiên

### Requirement: Phản hồi và tiếp nối không gây áp lực
Prototype SHALL nhận kết quả làm, làm một phần hoặc chưa làm và một chỉ dẫn do người chơi chủ động chọn cho lượt sau; phản hồi SHALL cho thấy chỉ dẫn đó ảnh hưởng đề xuất tiếp theo như thế nào, không suy sở thích từ một hành vi, chấm điểm sức khỏe hoặc phạt ngày bỏ lỡ.

#### Scenario: Làm một phần
- **WHEN** người chơi báo đã làm một phần và muốn giảm tải lần sau
- **THEN** lượt sau bắt đầu bằng lựa chọn nhẹ hơn theo đúng chỉ dẫn họ vừa chọn, không ghi là thất bại toàn phần

#### Scenario: Bỏ lỡ một ngày
- **WHEN** người chơi quay lại sau một ngày không mở prototype
- **THEN** họ bắt đầu lượt mới bình thường, không phải bù nhiệm vụ hoặc sửa streak

### Requirement: Đường lùi khi đề xuất không đáng tin
Prototype SHALL cho phép chơi vòng cơ bản bằng lựa chọn được biên soạn sẵn hoặc hành động do người chơi tự chọn khi hệ thống không thể đưa đề xuất phù hợp; SHALL không suy luận bệnh hay khẳng định hoạt động sức khỏe an toàn khi thiếu dữ kiện.

#### Scenario: Dữ kiện sức khỏe khiến tính phù hợp không rõ
- **WHEN** người chơi cho biết một giới hạn hoặc triệu chứng khiến hoạt động được gợi ý không chắc phù hợp
- **THEN** prototype bỏ thẻ sức khỏe đó, không hỏi sâu hay đánh giá triệu chứng, và cho kết thúc lượt hoặc tự chọn một hành động đời thường quen thuộc; nếu vấn đề vượt phạm vi bản thử, prototype nói ngắn rằng nó không thể đánh giá sức khỏe và người chơi có thể tìm hỗ trợ phù hợp khi cần

#### Scenario: Dịch vụ đề xuất không khả dụng
- **WHEN** nguồn đề xuất tự động không phản hồi
- **THEN** người chơi vẫn có thể chọn từ thẻ soạn sẵn hoặc tự đặt một mission ngắn
