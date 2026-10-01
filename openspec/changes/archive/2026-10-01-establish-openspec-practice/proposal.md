# Proposal

## Why

Dự án đã cài OpenSpec nhưng chưa có hướng dẫn đủ rõ để agent chọn đúng workflow, dùng đúng lệnh đã cài và phân biệt giả thuyết sản phẩm với hành vi đã triển khai. Cần một quy ước ngắn, có thể kiểm chứng, trước khi bắt đầu xây game.

## What Changes

- Bổ sung skill riêng để quyết định khi nào và cách nào dùng OpenSpec cùng Superpowers.
- Cập nhật `AGENTS.md` để định rõ trách nhiệm của tài liệu sản phẩm, spec hiện hành, change đang mở, mã nguồn và nghiên cứu riêng tư.
- Ghi cách gọi các skill Codex và CLI OpenSpec thật trong README.
- Kiểm tra skill, CLI và quy trình change bằng các lệnh của bản OpenSpec đang ghim.

## Capabilities

### New Capabilities

Không có. Đây là thay đổi về tài liệu và công cụ làm việc, chưa tạo hành vi trong game.

### Modified Capabilities

Không có. Change này khai báo `skip_specs: true`.

## Impact

`AGENTS.md`, `.agents/skills/using-openspec/SKILL.md`, `README.md` và tài liệu vận hành trong repo. Không đổi dependency hay lựa chọn công nghệ chạy game.
