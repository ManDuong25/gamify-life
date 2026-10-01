# Design

## Context

Dự án chưa có ứng dụng chơi được, đặc tả game hiện hành hoặc nền tảng sản phẩm đã chọn. Xem [proposal.md](proposal.md) để biết mục đích. Hướng cảm xúc cho bản thử đầu là **hành trình hồi phục và khám phá**, do chủ sản phẩm chọn. Các cơ chế cụ thể dưới đây là giả thuyết prototype, chỉ trở thành hướng sản phẩm sau playtest và quyết định tiếp theo.

## Goals / Non-Goals

**Goals:**

- Có một luồng ngắn mà người chơi hiểu và tự hoàn tất: định hướng → nhận/sửa mission → hành động ngoài đời → phản hồi → thấy dấu vết cho lượt sau.
- So sánh tác dụng của thẻ mission thường với nhánh chọn ưu tiên khi có xung đột thật, trên cả giá trị hành động và cảm giác chơi.
- Kiểm tra các đường lùi: ít sức, thiếu dữ kiện, đề xuất sai, bỏ lỡ ngày, dịch vụ đề xuất không hoạt động và giới hạn sức khỏe chưa rõ.
- Có hồ sơ playtest ghi điều quan sát được, điều người chơi nói, lỗi và quyết định đi tiếp/sửa/dừng.

**Non-Goals:**

- Chứng minh hiệu quả sức khỏe, thói quen dài hạn hoặc khả năng giữ chân qua một prototype ngắn.
- Xây AI trực tiếp, tài khoản, đồng bộ, wearable, cơ sở dữ liệu người dùng, XP, streak, shop, avatar, chẩn đoán hay chương trình vận động.
- Chọn web hay mobile làm nền tảng phát hành. Prototype có thể chạy trong trình duyệt để thử nhanh mà không khóa công nghệ sản phẩm.

## Decisions

### 1. Một vòng nền, một nhánh xung đột

Luồng mặc định dùng **Mission Card**: hiện một việc có bước đầu, điều kiện xong và lý do ngắn; quyết định chính chỉ là nhận hoặc mở nhóm điều chỉnh/bỏ qua. Nhóm thứ hai chứa giảm tải, thay, tự đặt, hoãn và từ chối, không dồn mọi nút lên thẻ đầu. **Priority Clash** chỉ xuất hiện khi người chơi xác nhận cả deadline, ưu tiên khác muốn bảo vệ và xung đột thật trong quỹ sức/thời gian. Khi đó hiện hai hướng hành động ngắn, cho người chơi chọn trước khi hiện mission tương ứng. Cả hai nhánh cùng dùng bước thực hiện và phản hồi. Lựa chọn này giảm số quyết định thường ngày so với việc đưa 2–3 phương án mỗi lượt, nhưng vẫn có quyết định chơi khi đánh đổi là thật.

### 2. Prototype tương tác thấp với nội dung soạn sẵn

Làm một bản web tĩnh nhỏ trong `prototype/` bằng HTML/CSS/JavaScript, mở trên thiết bị người thử, dùng thẻ mission và kỹ năng soạn sẵn cho các tình huống cố định. Người điều phối có thể chuyển “ngày” và kích hoạt tình huống trong bản thử. Không đưa dữ liệu thật hoặc thông tin cá nhân vào fixture công khai; trạng thái thử chỉ cần tồn tại trong phiên chơi và có thể đặt lại. Nội dung soạn sẵn cho phép quan sát vòng chơi trước khi chi phí và sai số của AI che mất vấn đề thiết kế. Đây là phương tiện playtest, không phải quyết định nền tảng sản phẩm.

### 3. Dấu vết hành trình là trạng thái nhỏ nhất

Một lượt chỉ cần giữ: hướng người chơi đang bảo vệ, kết quả mission gần nhất (`đã làm`, `một phần`, `chưa làm`) và **chỉ dẫn người chơi tự chọn** cho lượt sau (`giữ`, `nhẹ hơn`, `khác`, `tự chọn`). Không suy ra sở thích bền vững từ một lượt. Màn phản hồi cho thấy quan hệ nhân quả cụ thể, chẳng hạn “Bạn đã chọn nhẹ hơn → lượt này bắt đầu nhẹ hơn”; không gán điểm giá trị con người, điểm sức khỏe hay nợ nhiệm vụ. Cần playtest xem đây là tiến trình game có ý nghĩa hay chỉ là lịch sử việc.

### 4. Kỹ năng là hành trình tự nguyện

Prototype cho chọn từ một nhóm gợi ý kỹ năng khác nhau, hoặc chọn “chưa muốn”. Growth Mission chỉ mở khi người chơi chọn xem hoặc đồng ý nhận gợi ý thêm; bỏ qua và đổi kỹ năng không có hình phạt. Danh sách cụ thể và nhịp gợi ý có thể chỉnh sau playtest. AI gợi ý kỹ năng là khả năng tương lai, không phải điều kiện của vòng chơi bản thử.

### 5. Ranh giới đề xuất và đường lùi

Các thẻ sức khỏe là hành động đời thường, mang tính lựa chọn, không suy luận triệu chứng hay kê cường độ/tần suất như điều trị. Nếu tính phù hợp không rõ, bản thử bỏ thẻ đó, không hỏi sâu hay đổi sang một bài vận động khác; người chơi có thể kết thúc lượt hoặc tự chọn một hành động đời thường quen thuộc. Nếu họ nêu vấn đề vượt phạm vi, bản thử nói ngắn rằng nó không thể đánh giá sức khỏe và họ có thể tìm hỗ trợ phù hợp khi cần. Chữ của đường lùi này phải được rà trước playtest, và chuyên gia cần rà an toàn trước khi mở rộng công khai. Khi thiếu dữ kiện hoặc dịch vụ đề xuất lỗi, người chơi vẫn đi tiếp bằng thẻ trung tính hoặc mission tự đặt. Sau ngày bỏ lỡ, lượt mới mở bình thường. Prototype không hỏi nỗi sợ như câu cố định; chỉ hỏi khi chướng ngại thực sự có thể đổi mission và cho bỏ qua.

### 6. Playtest theo cổng quyết định

Chuẩn bị kịch bản cho ít nhất: ngày ít sức; cùng thời gian nhưng mức sức khác; deadline có xung đột thật và deadline không có xung đột; mission sai; bỏ lỡ; thiếu dữ kiện/giới hạn sức khỏe; dịch vụ đề xuất lỗi; skill bị bỏ qua. Người đầu tiên tự thử để bắt lỗi rõ, sau đó cần ít nhất một người khác gần nhóm mục tiêu tự đi hết vòng mà người điều phối không giải thích hộ trước khi có thể kết luận đi tiếp sang vertical slice. Ghi riêng **hành động có ích ngoài đời** và **trải nghiệm chơi**: họ hiểu quyền sửa, có chọn phù hợp, có bắt đầu hoặc từ chối có chủ đích, thấy lựa chọn được nhớ, muốn thử lượt sau, có cảm giác bị ép hay không. Chi tiết deadline và bối cảnh cá nhân chỉ lưu trong `research/`; báo cáo công khai chỉ nêu loại xung đột không nhận dạng. Các kịch bản sức khỏe không được dùng để thử lời khuyên y tế.

Đi tiếp sang vertical slice chỉ khi có quan sát ngoài chủ sản phẩm như trên, người chơi tự hiểu luồng, quyết định có ý nghĩa, đường lùi hoạt động và có tín hiệu muốn quay lại vì trạng thái hành trình. Nếu chưa có người ngoài thử, kết quả là **giữ để thử tiếp**, không phải “đi tiếp”. Nếu có ích nhưng không có cảm giác chơi, sửa phần quyết định/phản hồi trước. Nếu cả giá trị đời thật lẫn trải nghiệm đều yếu, dừng giả thuyết vòng chơi này. Không đặt ngưỡng hiệu quả sức khỏe từ mẫu playtest nhỏ.

### Căn cứ và giới hạn

[COM-B](https://pmc.ncbi.nlm.nih.gov/articles/PMC3096582/) giúp xem khả năng, cơ hội và động lực có thể thay đổi lựa chọn hành động; [khung JITAI](https://pmc.ncbi.nlm.nih.gov/articles/PMC5364076/) gợi ý xác định điểm quyết định, dữ kiện và quy tắc thích ứng. [Tổng hợp thử nghiệm game hóa vận động](https://pmc.ncbi.nlm.nih.gov/articles/PMC8767479/) thấy hiệu ứng trung bình nhỏ đến vừa trong bối cảnh nghiên cứu nhưng yếu hơn ở theo dõi dài hạn; không chứng minh game này hiệu quả. [WHO](https://www.who.int/health-topics/noncommunicable-diseases/physical-activity) khuyên người ít vận động bắt đầu từ lượng phù hợp rồi tăng dần, không hỗ trợ một ngưỡng nhiệm vụ chung cho mọi người. [Unity](https://learn.unity.com/course/design-and-publish-your-original-game-unity-usc-games-unlocked/unit/milestones) phân biệt milestone prototype/vertical slice trong sản xuất game. Đây là căn cứ để thiết kế phép thử và ranh giới, không phải chứng nhận cho cơ chế cụ thể.

## Risks / Trade-offs

- **Dấu vết hành trình chỉ giống nhật ký việc** → thử khả năng người chơi tự kể điều đã thay đổi và có muốn xem lượt sau; sửa vòng quyết định trước khi thêm điểm thưởng.
- **Nhánh xung đột làm tăng căng thẳng hoặc ép chọn sai** → chỉ hiện khi hai ưu tiên được xác nhận, dùng lời trung tính, luôn cho đổi/hoãn.
- **AI hoặc thẻ soạn sẵn gợi ý hoạt động không phù hợp** → không đưa lời khuyên lâm sàng, lọc thẻ theo giới hạn đã biết và giữ quyền tự chọn/bỏ qua.
- **Prototype tạo ảo giác cá nhân hóa** → ghi rõ nội dung là kịch bản soạn sẵn; không suy hiệu quả thật từ lời khen trong buổi chơi.
- **Mẫu thử nhỏ và thiên lệch vì người đầu là chủ sản phẩm** → dùng vòng tự thử để tìm lỗi rõ, rồi quan sát thêm người gần đối tượng trước khi chốt vertical slice.

## Migration Plan

Không có dữ liệu hoặc ứng dụng hiện hành để chuyển đổi. Sau khi chủ sản phẩm duyệt, thực hiện prototype và lưu bằng chứng playtest; chỉ tạo kế hoạch vertical slice riêng nếu qua cổng quyết định. Nếu thất bại, giữ kết quả nghiên cứu và sửa hoặc đóng change theo thực tế, không đồng bộ đặc tả thành hành vi hiện hành.

## Open Questions

- Hình ảnh ẩn dụ cụ thể của hành trình, chữ phản hồi và số kỹ năng gợi ý sẽ được chọn sau khi thử vài bản trình bày; chúng không đổi hành vi cốt lõi ở đặc tả này.
- AI provider, mô hình, nền tảng phát hành và lưu dữ liệu dài hạn chỉ cần chọn khi vòng chơi được chứng minh đủ rõ để làm vertical slice.
