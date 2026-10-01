# Design

## Context

Xem `proposal.md`. Repo đã ghim OpenSpec v1.14.0 và sinh sáu skill Codex trong `.agents/skills/openspec-*`. Các file này do CLI quản lý. Repo còn có các skill Superpowers cho thiết kế, triển khai và kiểm chứng.

## Goals / Non-Goals

**Goals:** Có một nơi ngắn gọn hướng dẫn quyết định khi nào dùng OpenSpec, và một `AGENTS.md` phân vai các nguồn thông tin cùng skill.

**Non-Goals:** Không thay schema OpenSpec, không tạo spec tính năng game khi game chưa có implementation, không chỉnh trực tiếp skill do OpenSpec sinh.

## Decisions

- Đặt skill tự viết ở `.agents/skills/using-openspec/` để Codex khám phá theo dự án và tránh tiền tố `openspec-*` được CLI tái tạo. Phương án sửa skill sinh sẵn dễ mất khi `openspec update`.
- Giữ `AGENTS.md` là quy tắc dự án và skill tự viết là hướng dẫn dùng OpenSpec có thể tái dùng. Phương án đưa toàn bộ quy trình vào `AGENTS.md` gây trùng lặp với skill sinh sẵn.
- Dùng change `skip_specs: true` vì đây là thay đổi tooling/tài liệu, không đổi hành vi game. Phương án tạo delta spec giả để validate là sai ngữ nghĩa.
- Dùng CLI cài thật để tạo change, lấy instructions và validate. Riêng change này kiểm tra lệnh terminal `openspec archive` sau khi các tác vụ hoàn tất; skill archive do OpenSpec sinh là một workflow agent riêng. Nội dung Markdown vẫn được biên soạn theo instructions; CLI không tự viết nội dung đó.

## Risks / Trade-offs

- Skill tự viết có thể trùng các skill OpenSpec → Giữ phạm vi ở chọn workflow và tiêu chí đồng bộ, giao thao tác cho skill sinh sẵn.
- Quy tắc quá dài làm agent khó theo → Giữ `AGENTS.md` ngắn, dẫn tới skill và tài liệu chính thức.
- Tài liệu công khai có thể lộ ngữ cảnh riêng → Chỉ đưa các file công khai đã rà vào phản biện độc lập và kiểm tra diff trước khi lưu.

## Migration Plan

Không có migration runtime. Sau khi kiểm chứng, archive change bằng CLI và giữ tài liệu/skill trong Git.
