# AI Agent Guide

## Prompt mẫu: phân tích requirement

```text
Hãy đọc toàn bộ docs/requirements và cho tôi biết requirement nào đã Ready for Dev, requirement nào còn blocker. Không code.
```

## Prompt mẫu: lập plan cho feature

```text
Hãy đọc:
- docs/ai/project-context.md
- docs/ai/coding-rules.md
- docs/requirements/reqs/HR-CONTRACT-001-tao-hop-dong-lao-dong.md
- docs/specs/01-hr-contracts/software-design-spec.md

Sau đó lập implementation plan chi tiết cho module HR Contracts. Chưa code.
Nếu thấy thiếu thông tin hoặc rule mâu thuẫn, hãy liệt kê rõ.
```

## Prompt mẫu: code theo spec

```text
Triển khai module HR Contracts theo software-design-spec.md.
Yêu cầu:
- Tuân thủ coding-rules.md.
- Không đổi kiến trúc hiện tại.
- Nếu entity đã tồn tại thì cập nhật thay vì tạo mới trùng lặp.
- Sau khi code, liệt kê file đã thay đổi và test cần chạy.
```

## Prompt mẫu: review output của AI/dev

```text
Hãy review code thay đổi so với các requirement:
- HR-CONTRACT-001
- HR-SALARY-001

Kiểm tra:
- Business rules có đủ không?
- API contract có đúng không?
- Edge cases có thiếu không?
- Test cases có bao phủ acceptance criteria không?
```
