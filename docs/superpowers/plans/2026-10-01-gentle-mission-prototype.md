# Gentle Mission Prototype Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Xây một prototype ngắn để kiểm tra liệu vòng “chọn một mission vừa sức → hành động ngoài đời → thấy lựa chọn ảnh hưởng lượt sau” có vừa hữu ích vừa có cảm giác game.

**Architecture:** Web tĩnh nhỏ với dữ liệu tình huống soạn sẵn. Logic chọn mission và chuyển trạng thái là các hàm thuần có thể kiểm thử; lớp giao diện chỉ hiển thị và nhận thao tác. Không gọi AI hoặc lưu dữ liệu cá nhân.

**Tech Stack:** HTML, CSS, JavaScript ES modules (`.mjs`), Node built-in test runner; chạy prototype bằng HTTP server tĩnh cục bộ. Đây là công cụ thử thiết kế, không chốt nền tảng sản phẩm.

**Spec:** [OpenSpec change](../../../openspec/changes/prototype-gentle-mission-loop/proposal.md), [delta daily loop](../../../openspec/changes/prototype-gentle-mission-loop/specs/daily-mission-loop/spec.md), [delta skill journey](../../../openspec/changes/prototype-gentle-mission-loop/specs/optional-skill-journey/spec.md), [design](../../../openspec/changes/prototype-gentle-mission-loop/design.md); `tasks.md` là checklist trạng thái chuẩn khi thực thi.

## Global Constraints

- Đây là bản thử tương tác thấp, chưa phải game hoàn thiện hoặc can thiệp sức khỏe được chứng minh.
- Một Main Mission tại một thời điểm; Growth Mission tự nguyện. Quyết định chính trên thẻ là **Nhận** hoặc **Điều chỉnh / bỏ qua**; các lựa chọn khác nằm trong nhóm thứ hai.
- Priority Clash chỉ xuất hiện khi người chơi xác nhận deadline, ưu tiên khác muốn bảo vệ và xung đột thật trong sức/thời gian hiện có.
- Trạng thái tiếp nối chỉ gồm hướng hiện tại, outcome gần nhất và chỉ dẫn người chơi tự chọn cho lượt sau; không suy ra đặc tính con người, không XP/streak/điểm sức khỏe.
- Nội dung công khai dùng tình huống giả lập, không ghi chi tiết sức khỏe, công việc hoặc deadline thật của người tham gia. Ghi chép cá nhân ở `research/`.
- Không chẩn đoán, đánh giá triệu chứng hoặc kê bài tập. Khi tính phù hợp không rõ, bỏ thẻ sức khỏe và cho kết thúc hoặc tự chọn hành động đời thường quen thuộc.
- Chỉ có owner self-test thì quyết định tối đa là `giữ để thử tiếp`, không là `đi tiếp` sang vertical slice.

## Review Focus

1. Deadline có thật nhưng không có xung đột: không xuất hiện Priority Clash; kiểm bằng `mission.test.mjs` ở Task 2.
2. Mission không phù hợp hoặc thông tin sức khỏe không rõ: không tự thay bằng bài vận động khác; kiểm bằng `mission.test.mjs` ở Task 2 và clickthrough ở Task 4.
3. Bỏ lỡ một ngày: không có nợ, reset hay lời trách; kiểm bằng `journey.test.mjs` ở Task 3 và clickthrough ở Task 4.
4. Người chơi chưa chọn kỹ năng: Main Mission vẫn trọn vẹn; kiểm bằng `skills.test.mjs` ở Task 3.
5. Không có người ngoài owner thử: báo cáo không được ghi `đi tiếp`; kiểm bằng mẫu cổng quyết định ở Task 6.

---

### Task 1: Nội dung giả lập và ma trận tình huống

**Files:** Create `prototype/content.mjs`, `prototype/content.test.mjs`, `prototype/README.md`.

**Interfaces:** `getScenario(id: string)` trả về bối cảnh giả lập có `priority`, `time`, `energy`, `deadline`, `confirmedConflict`, `healthSuitability`; `getMissionCard(id: string)` trả về thẻ với `action`, `firstStep`, `doneWhen`, `reason`, `lighterCardId`. Mọi ID ổn định để các task sau dùng.

- [ ] **Step 1:** Viết `content.test.mjs` cho các ID tình huống trong OpenSpec task 1.1; assert thẻ được tham chiếu tồn tại, có bước đầu và dấu hiệu hoàn tất.
- [ ] **Step 2:** Chạy `node --test prototype/content.test.mjs`; xác nhận fail vì module/nội dung chưa có.
- [ ] **Step 3:** Tạo `content.mjs` với thẻ soạn sẵn và `prototype/README.md` nêu từng scenario, mục đích thử và cách đặt lại dữ liệu.
- [ ] **Step 4:** Chạy lại test, rà thủ công chữ thẻ theo ranh giới sức khỏe và kiểm tra không có dữ kiện thật của người dùng, ghi kết quả rà ở README; cập nhật checkbox 1.1–1.2 trong OpenSpec tasks theo bằng chứng.
- [ ] **Step 5:** Commit riêng nội dung giả lập sau khi kiểm tra diff công khai không chứa thông tin cá nhân.

### Task 2: Quy tắc đề xuất, quyền sửa và nhánh xung đột

**Files:** Create `prototype/mission.mjs`, `prototype/mission.test.mjs`; use `prototype/content.mjs`.

**Interfaces:** `proposeMain(context, state, catalog)` trả về `{kind: 'mission'|'tradeoff'|'manual', missionId?, options?, reason}`. `chooseMission(proposal, action, replacement?)` nhận `replacement` là `{missionId?: string, selfWrittenAction?: string}` và trả về `{status: 'active'|'deferred'|'declined', missionId?, selfWrittenAction?}`. Logic không đọc DOM và không gọi mạng.

- [ ] **Step 1:** Viết test cho bối cảnh đủ/thiếu, deadline có và không có xung đột, nhận/giảm/thay/tự đặt/hoãn/từ chối, và tính phù hợp sức khỏe không rõ; assert đúng `kind` và không có bài vận động thay thế tự động.
- [ ] **Step 2:** Chạy `node --test prototype/mission.test.mjs`; xác nhận fail có ý nghĩa.
- [ ] **Step 3:** Viết logic tối thiểu để đáp ứng spec; giữ nhánh tradeoff chỉ khi cả ba điều kiện đã được xác nhận, và trả `manual` khi không có thẻ đáng tin.
- [ ] **Step 4:** Chạy lại test; đối chiếu từng scenario trong `daily-mission-loop/spec.md` với một case và ghi bằng chứng logic. Chưa đánh dấu các OpenSpec task đòi hành vi trên trình duyệt trước Task 4.
- [ ] **Step 5:** Commit logic cùng test.

### Task 3: Trạng thái hành trình và kỹ năng tùy chọn

**Files:** Create `prototype/journey.mjs`, `prototype/journey.test.mjs`, `prototype/skills.mjs`, `prototype/skills.test.mjs`.

**Interfaces:** `recordTurn(state, outcome, nextInstruction)` trả về `{path, lastOutcome, nextInstruction}`; `nextInstruction` chỉ được lấy từ lựa chọn người chơi. `selectSkill(currentSkillId, selectedSkillId|null)` và `offerGrowth(selectedSkillId, optedIn)` không làm thay đổi khả năng hoàn thành Main Mission.

- [ ] **Step 1:** Viết test cho `đã làm`/`một phần`/`chưa làm`, ngày bỏ lỡ, chỉ dẫn `giữ`/`nhẹ hơn`/`khác`/`tự chọn`, chọn/không chọn/đổi kỹ năng, và bỏ qua/tạm dừng Growth Mission; assert không suy sở thích từ outcome và không tạo streak/debt. Thêm case nối `recordTurn` → `proposeMain`: chọn `nhẹ hơn` phải làm đề xuất lượt sau bắt đầu bằng thẻ nhẹ hơn.
- [ ] **Step 2:** Chạy `node --test prototype/journey.test.mjs prototype/skills.test.mjs`; xác nhận fail.
- [ ] **Step 3:** Viết các hàm thuần và dữ liệu kỹ năng giả lập đủ để mở một Growth Mission tự nguyện.
- [ ] **Step 4:** Chạy lại test và đối chiếu hai delta spec; ghi bằng chứng logic, để các OpenSpec task có acceptance giao diện chờ clickthrough ở Task 4.
- [ ] **Step 5:** Commit trạng thái cùng test.

### Task 4: Giao diện có thể chơi và đường lùi

**Files:** Create `prototype/index.html`, `prototype/styles.css`, `prototype/app.mjs`; update `prototype/README.md`.

**Interfaces:** `app.mjs` nối các hàm ở Tasks 1–3 với màn định hướng, thẻ mission, nhóm điều chỉnh, nhánh xung đột, phản hồi, dấu vết và kỹ năng; không có logic chọn/safety mới trong DOM layer.

- [ ] **Step 1:** Dựng giao diện tĩnh với chữ và thao tác rõ; đặt các lựa chọn thứ cấp sau nút Điều chỉnh / bỏ qua; cho người điều phối đổi fixture và “ngày”.
- [ ] **Step 2:** Chạy `python3 -m http.server 8765 --directory prototype`, mở bằng trình duyệt và đi qua ma trận: đủ context → không hỏi lại; thiếu context → Bỏ qua → tự chọn hành động; deadline không xung đột → không có Priority Clash; chọn `nhẹ hơn` → lượt sau hiện thẻ nhẹ hơn; bỏ qua/tạm dừng Growth Mission → không có việc tồn. Xác nhận đường lùi hiển thị giới hạn của prototype khi tính phù hợp sức khỏe không rõ.
- [ ] **Step 3:** Kiểm tra trên màn nhỏ và màn thường, điều khiển bàn phím, nhịp đọc tự chọn và không có chuyển động bắt buộc; ghi lỗi và kết quả sửa trong README.
- [ ] **Step 4:** Chạy `node --test prototype/*.test.mjs` và `npm exec -- openspec validate prototype-gentle-mission-loop --strict`; chỉ lúc này đánh dấu OpenSpec tasks 2.1–2.5, 3.1–3.3 theo từng bằng chứng test/clickthrough tương ứng.
- [ ] **Step 5:** Commit bản có thể chơi cùng tài liệu mở và kết quả smoke test.

### Task 5: Bộ playtest

**Files:** Create `docs/playtests/gentle-mission-protocol.md`; update `prototype/README.md` nếu kịch bản cần lời dẫn.

**Interfaces:** Mẫu quan sát có trường `scenario`, `observedChoice`, `outsideAction`, `gameExperience`, `friction`, `safetyConcern`, `participantQuotePrivateRef`; không chứa thông tin nhận dạng trong bản công khai.

- [ ] **Step 1:** Viết quy trình để người thử tự thao tác, các câu hỏi sau lượt, cách ghi riêng hành động có ích và cảm giác chơi; đối chiếu ma trận tình huống, đảm bảo có cả deadline không xung đột.
- [ ] **Step 2:** Tự thử toàn bộ kịch bản để bắt lỗi rõ; xác nhận câu hỏi không gợi ý câu trả lời và báo cáo tự thử không tự kết luận hiệu quả.
- [ ] **Step 3:** Commit mẫu playtest và sửa lỗi phát hiện; cập nhật OpenSpec task 4.1.

### Task 6: Quan sát ngoài chủ sản phẩm và quyết định cổng

**Files:** Store raw notes in `research/` (gitignored); create/update `docs/playtests/gentle-mission-findings.md` with non-identifying summary.

**Interfaces:** Gate outcome is one of `đi tiếp`, `sửa`, `dừng`, `giữ để thử tiếp` with evidence for real-world usefulness, game feel, fallback behavior and who was observed. No numerical health-effect claim.

- [ ] **Step 1:** Quan sát ít nhất một người gần nhóm mục tiêu tự hoàn thành core loop mà người điều phối không giải thích hộ; nếu chưa có người tham gia, ghi `giữ để thử tiếp` và chờ playtest trước khi xét vertical slice.
- [ ] **Step 2:** Ghi raw notes riêng trong `research/`; viết kết quả công khai không có chi tiết deadline, sức khỏe hay nhận dạng, rồi đối chiếu với raw notes.
- [ ] **Step 3:** Đánh giá theo cổng trong OpenSpec design; nêu lỗi, điều đã sửa và quyết định có căn cứ. Chạy `git diff --check`, kiểm tra `git ls-files research` rỗng; cập nhật OpenSpec tasks 4.2–4.3.
- [ ] **Step 4:** Chỉ sau quyết định `đi tiếp`, lập change khác cho vertical slice; prototype này không tự động biến thành đặc tả sản phẩm đã được chứng minh.

## Execution boundary

Kế hoạch này chờ chủ sản phẩm duyệt. Việc duyệt cho phép xây **prototype và playtest theo các task trên**; quyết định làm vertical slice là một cổng riêng sau khi xem kết quả. Không có mã game nào được triển khai trong lần lập kế hoạch này.
