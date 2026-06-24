# Project Context for AI Agent

## Dự án mẫu

HR Management System là hệ thống quản lý nhân sự, tập trung vào hồ sơ nhân viên, hợp đồng lao động, lịch sử lương và lịch sử BHXH.

## Mục tiêu hiện tại

Triển khai module quản lý hợp đồng lao động giai đoạn v1.0:

- HR tạo được hợp đồng lao động.
- Hệ thống kiểm tra rule nghiệp vụ chính.
- Hệ thống tự tạo lịch sử lương khi hợp đồng có BaseSalary hợp lệ.

## Source of Truth

AI agent phải ưu tiên đọc requirement tại:

```text
docs/requirements/
```

Thứ tự ưu tiên khi có mâu thuẫn:

1. `docs/requirements/reqs/*.md`
2. `docs/requirements/business-rules.md`
3. `docs/requirements/stakeholder-decisions.md`
4. `docs/specs/*/software-design-spec.md`
5. Prompt trực tiếp của người dùng

Nếu prompt trái với source requirement, AI agent phải cảnh báo và hỏi lại hoặc ghi vào `open-questions.md`.

## Cách làm việc mong muốn

1. Đọc context.
2. Đọc requirement liên quan.
3. Đọc software design spec.
4. Lập implementation plan.
5. Chỉ code sau khi plan rõ.
6. Nếu thiếu thông tin, cập nhật `docs/requirements/open-questions.md`.
7. Sau khi code, cập nhật validation report nếu được yêu cầu.
