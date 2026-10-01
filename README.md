# Gamify Life

Ý tưởng game giúp người bận rộn chọn một hành động có ý nghĩa, vừa sức mỗi ngày và khám phá một kỹ năng do chính họ chọn. Dự án đang ở giai đoạn khám phá/tiền sản xuất; chưa có bản game chơi được.

**Đang chờ chủ sản phẩm duyệt:** [OpenSpec change cho prototype vòng chơi](openspec/changes/prototype-gentle-mission-loop/proposal.md) và [kế hoạch triển khai, kiểm chứng](docs/superpowers/plans/2026-10-01-gentle-mission-prototype.md). Chưa triển khai prototype; kết quả playtest mới quyết định có làm vertical slice hay không.

## Bắt đầu từ đâu

- [Tóm tắt sản phẩm công khai](docs/PRODUCT_BRIEF.md): hướng sản phẩm và các quyết định còn mở.
- `research/GAME_PRODUCT_PLAN.md`: kế hoạch đầy đủ trên máy, nếu có. Thư mục này không được đưa lên Git vì chứa bối cảnh cá nhân.
- [Các thay đổi OpenSpec](openspec/changes): đề xuất, yêu cầu, thiết kế và tác vụ theo từng thay đổi. [Đặc tả chính](openspec/specs) mô tả hành vi hiện hành được chấp nhận; hiện chưa có tính năng game để ghi ở đây.
- [Hướng dẫn cho agent](AGENTS.md): vai trò các nguồn thông tin và quy tắc dự án.
- [Skill dùng OpenSpec](.agents/skills/using-openspec/SKILL.md): chọn phạm vi thay đổi và phối hợp OpenSpec với các skill khác.

## Quy trình làm việc cùng AI

Repo dùng [OpenSpec](https://github.com/Fission-AI/OpenSpec) **v1.14.0** làm bộ khung quản lý thay đổi. Nó hỗ trợ Codex và giữ đề xuất, tình huống kiểm chứng, thiết kế cùng tác vụ của mỗi thay đổi ở một nơi. Skill cho Codex ở `.agents/skills/`. CLI được ghim phiên bản trong dependency phát triển; dự án chưa chọn công nghệ chạy ứng dụng.

```bash
npm ci
npm run spec:doctor
npm run spec:list
```

Trong **Codex chat**, dùng `$using-openspec` khi cần chọn quy trình; `$openspec-explore` để làm rõ ý tưởng và `$openspec-propose` khi đã có thay đổi đủ cụ thể. Các skill do CLI sinh còn có `$openspec-apply-change`, `$openspec-update-change`, `$openspec-sync-specs` và `$openspec-archive-change`. Tài liệu OpenSpec thường viết `/opsx:*` cho những công cụ hỗ trợ slash command; Codex trong repo này dùng tên skill `$openspec-*`.

Trong **terminal**, dùng CLI đã cài từ `package-lock.json`, không gõ các tên skill vào shell:

```bash
npm exec -- openspec --version
npm exec -- openspec list
npm exec -- openspec doctor
npm exec -- openspec validate --all --strict
```

Để bắt đầu một thay đổi, dùng lệnh terminal `npm exec -- openspec new change TEN_CHANGE`; thay `TEN_CHANGE` bằng tên thật ở dạng kebab-case. Sau đó dùng `status --change TEN_CHANGE` và `instructions proposal --change TEN_CHANGE` của CLI để biết artifact nào cần viết và viết theo template mà CLI trả về. Các lệnh này đã được chạy thật với change `establish-openspec-practice` trong repo. CLI cung cấp cấu trúc và hướng dẫn; người làm việc vẫn phải biên soạn nội dung proposal, spec, design, tasks theo hướng dẫn đó. Trước khi archive, kiểm tra bằng chứng phù hợp với thay đổi: file và lệnh cho thay đổi tài liệu/công cụ, kiểm thử và hành vi quan sát được cho tính năng game. `validate` chỉ kiểm tra cấu trúc, không chứng minh game đã chạy đúng. Xem [hướng dẫn chính thức v1.14.0](https://github.com/Fission-AI/OpenSpec/blob/v1.14.0/docs/README.md).

**Lý do chọn:** [repository-harness](https://github.com/hoangnb24/repository-harness) có quy tắc repo và cơ chế cập nhật cẩn thận nhưng không có luồng đặc tả tính năng; [Spec Kit](https://github.com/github/spec-kit) có quy trình nhiều bước hơn; [BMad Game Dev Studio](https://github.com/bmad-code-org/bmad-module-game-dev-studio) thêm quy trình sản xuất game. Cách ghi thay đổi gọn, lặp được và hỗ trợ Codex của OpenSpec hợp với giai đoạn hiện tại. Đây là các lựa chọn thay thế, không phải dependency của dự án.

Việc cần chứng minh đầu tiên là vòng chơi nhiệm vụ nhỏ nhất. Chỉ chọn web/mobile và công nghệ chạy ứng dụng sau khi thử trải nghiệm đó.
