# Coding Rules for AI Agent

> File mẫu. Khi áp dụng vào dự án thật, sửa theo convention của source code hiện tại.

## General Rules

- Không tự ý thay đổi kiến trúc dự án.
- Không tự ý đổi tên entity/table/field đã tồn tại.
- Không tạo duplicate entity nếu project đã có entity tương đương.
- Không hard-code business rule nếu rule đang ở trạng thái Draft/Open.
- Không bỏ qua validation đã được định nghĩa trong requirement.
- Nếu phát hiện thiếu thông tin, ghi vào `docs/requirements/open-questions.md`.

## .NET Backend Rules

- Dùng async/await cho database operation.
- Không để business logic quan trọng trong controller nếu project dùng CQRS/Clean Architecture.
- Response/error phải theo convention hiện tại của project.
- Validation nên nằm ở command validator hoặc application layer tùy kiến trúc.
- Migration phải tương thích database hiện tại.

## Documentation Update Rules

Sau khi thay đổi code liên quan requirement:

- Cập nhật `change-log.md` nếu requirement thay đổi.
- Cập nhật `validation-report.md` nếu đã test.
- Cập nhật `open-questions.md` nếu còn điểm chưa rõ.
