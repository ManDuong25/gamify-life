# Tasks

## 1. Nghiên cứu và định phạm vi

- [x] 1.1 Đối chiếu tài liệu OpenSpec v1.14.0 với bản CLI đã cài; xác nhận `npm exec -- openspec --version` và các lệnh `list`, `status`, `instructions` chạy đúng.
- [x] 1.2 Phản biện độc lập nhiều vòng về cách phối hợp skill và ranh giới công khai/riêng tư, chỉ gửi artifact công khai; kiểm tra lại kết luận trên các file và lệnh thực tế.

## 2. Hướng dẫn agent

- [x] 2.1 Viết skill `using-openspec` với phạm vi không trùng skill sinh sẵn; chạy trình kiểm tra skill đã cài và thử tình huống chọn workflow độc lập.
- [x] 2.2 Cập nhật `AGENTS.md` về nguồn thông tin, routing, quyền và bằng chứng; rà độc lập và kiểm tra diff không lộ nghiên cứu riêng.
- [x] 2.3 Cập nhật README với cách gọi skill Codex và CLI thật; chạy lại các lệnh đã ghi trong README.

## 3. Kiểm tra tích hợp và kết thúc

- [x] 3.1 Trước khi archive, chạy `openspec validate` và `doctor`, rà checklist cùng diff công khai; xác nhận mọi tác vụ triển khai trong change đã hoàn tất. Sau đó có thể đánh dấu tác vụ này hoàn tất; bước archive và hậu kiểm được thực hiện ngoài checklist này.
