# Tasks

## 1. Kịch bản và nội dung thử

- [ ] 1.1 Viết ma trận tình huống trong `prototype/README.md` cho ngày ít sức, deadline có và không có xung đột, cùng thời gian khác mức sức, mission sai, ngày bỏ lỡ, thiếu dữ kiện, nguồn đề xuất lỗi và Growth Mission bị bỏ qua; đối chiếu từng tình huống với scenario trong hai delta spec.
- [ ] 1.2 Soạn bộ thẻ mission và gợi ý kỹ năng giả lập không chứa dữ liệu cá nhân, mỗi thẻ có bước đầu, điều kiện hoàn tất, lý do và lựa chọn nhẹ hơn; rà thủ công để không có ngưỡng vận động phổ quát, chẩn đoán hoặc lời hứa hiệu quả sức khỏe.

## 2. Vòng Main Mission

- [ ] 2.1 Dựng prototype web tĩnh trong `prototype/` cho định hướng ngắn và một thẻ Main Mission; chạy trên trình duyệt, xác nhận trường hợp đủ bối cảnh không hỏi lại và trường hợp thiếu bối cảnh cho bỏ qua.
- [ ] 2.2 Thêm quyết định chính nhận hoặc mở nhóm điều chỉnh/bỏ qua; trong nhóm thứ hai cho giảm tải, thay, tự đặt, hoãn và từ chối. Đi hết từng nhánh bằng trình duyệt, xác nhận không dồn mọi nút lên thẻ đầu và không có điểm phạt hoặc việc phải bù.
- [ ] 2.3 Thêm nhánh xung đột chỉ khi fixture xác nhận deadline, ưu tiên khác và đánh đổi thật; đi thử deadline có và không có xung đột, xác nhận chỉ case đầu hiện nhánh và mission theo lựa chọn người chơi.
- [ ] 2.4 Thêm phản hồi `đã làm`/`một phần`/`chưa làm`, chỉ dẫn do người chơi chọn và dấu vết nhân quả cho lượt sau; thử chuyển ngày và ngày bỏ lỡ, xác nhận không tự suy sở thích, không có streak hay nợ nhiệm vụ.
- [ ] 2.5 Ghi cách mở và đặt lại bản thử trong `prototype/README.md`; làm một lượt smoke test từ mở trang đến lượt kế tiếp trên màn hình nhỏ và màn hình thường, ghi kết quả trực tiếp trong README.

## 3. Đường lùi và hành trình kỹ năng

- [ ] 3.1 Dựng đường lùi khi mission không phù hợp, giới hạn sức khỏe chưa rõ hoặc nguồn đề xuất giả lập lỗi; đi thử từng fixture, xác nhận không hỏi sâu triệu chứng, không thay bằng bài vận động khác, có quyền kết thúc/tự chọn và có câu báo giới hạn của prototype khi vấn đề vượt phạm vi.
- [ ] 3.2 Thêm chọn kỹ năng từ danh sách biên soạn sẵn và Growth Mission tùy chọn; đi thử chọn, chưa chọn, bỏ qua, tạm dừng và đổi kỹ năng, xác nhận Main Mission luôn có thể kết thúc độc lập và không có việc tồn từ Growth Mission.
- [ ] 3.3 Rà chữ, khả năng đọc, điều khiển bằng bàn phím và chuyển động; quan sát trên prototype để xác nhận không có nội dung buộc đọc theo đồng hồ, hiệu ứng bắt buộc hoặc tín hiệu xấu hổ khi bỏ lỡ.

## 4. Playtest và cổng quyết định

- [ ] 4.1 Viết kịch bản quan sát và mẫu ghi chép tách hành động có ích, cảm giác chơi, sự rõ ràng, quyền đổi và tác dụng phụ; xác nhận mọi tình huống ở mục 1.1 có câu hỏi quan sát tương ứng, không đặt ngưỡng hiệu quả sức khỏe giả tạo.
- [ ] 4.2 Tự thử một vòng để tìm lỗi, rồi quan sát ít nhất một người ngoài chủ sản phẩm gần nhóm mục tiêu tự hoàn tất vòng mà không được giải thích hộ trước khi có thể xét `đi tiếp`; lưu chi tiết cá nhân và deadline trong `research/`, chỉ đưa kết quả không nhận dạng vào tài liệu công khai và đối chiếu tổng hợp với ghi chép gốc.
- [ ] 4.3 Ghi quyết định `đi tiếp`, `sửa`, `dừng` hoặc `giữ để thử tiếp` dựa trên hành vi quan sát, lỗi và hai lớp giá trị đời thật/game; nếu chỉ có owner test thì không chọn `đi tiếp`. Đối chiếu với cổng trong `design.md` trước khi đề xuất vertical slice, không đánh dấu prototype là đã chứng minh hiệu quả dài hạn.
