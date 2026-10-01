# Gamify Life

Ý tưởng game giúp người bận rộn chọn một hành động có ý nghĩa, vừa sức mỗi ngày và khám phá một kỹ năng do chính họ chọn. Dự án đang ở giai đoạn khám phá/tiền sản xuất; chưa có bản game chơi được.

## Bắt đầu từ đâu

- [Tóm tắt sản phẩm công khai](docs/PRODUCT_BRIEF.md): hướng sản phẩm và các quyết định còn mở.
- `research/GAME_PRODUCT_PLAN.md`: kế hoạch đầy đủ trên máy, nếu có. Thư mục này không được đưa lên Git vì chứa bối cảnh cá nhân.
- [Các thay đổi OpenSpec](openspec/changes): đề xuất, yêu cầu, thiết kế và tác vụ theo từng tính năng. [Đặc tả chính](openspec/specs) được cập nhật khi thay đổi được chấp nhận.
- [Hướng dẫn cho agent](AGENTS.md): thứ tự nguồn sự thật và quy tắc dự án.

## Quy trình làm việc cùng AI

Repo dùng [OpenSpec](https://github.com/Fission-AI/OpenSpec) **v1.14.0** làm bộ khung quản lý thay đổi. Nó hỗ trợ Codex và giữ đề xuất, tình huống kiểm chứng, thiết kế cùng tác vụ của mỗi thay đổi ở một nơi. Skill cho Codex ở `.agents/skills/`. CLI được ghim phiên bản trong dependency phát triển; dự án chưa chọn công nghệ chạy ứng dụng.

```bash
npm ci
npm run spec:doctor
npm run spec:list
```

Trong Codex, dùng `openspec-explore` để bàn một tính năng và `openspec-propose` để ghi thay đổi cụ thể. Rà lại yêu cầu và tình huống trước khi triển khai. Chạy CLI bằng `npm exec -- openspec <command>` trong repo này.

**Lý do chọn:** [repository-harness](https://github.com/hoangnb24/repository-harness) có quy tắc repo và cơ chế cập nhật cẩn thận nhưng không có luồng đặc tả tính năng; [Spec Kit](https://github.com/github/spec-kit) có quy trình nhiều bước hơn; [BMad Game Dev Studio](https://github.com/bmad-code-org/bmad-module-game-dev-studio) thêm quy trình sản xuất game. Cách ghi thay đổi gọn, lặp được và hỗ trợ Codex của OpenSpec hợp với giai đoạn hiện tại. Đây là các lựa chọn thay thế, không phải dependency của dự án.

Việc cần chứng minh đầu tiên là vòng chơi nhiệm vụ nhỏ nhất. Chỉ chọn web/mobile và công nghệ chạy ứng dụng sau khi thử trải nghiệm đó.
