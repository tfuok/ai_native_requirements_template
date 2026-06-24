# AI-native BA Requirements Template

Template này dùng để quản lý requirement theo mô hình:

```text
Requirement Source of Truth
→ Stakeholder Confirmation
→ Software Design Spec cho Dev/AI Agent
→ Implementation / UAT
→ Change Log
→ Update Source of Truth
```

Ngôn ngữ nội dung requirement: **Tiếng Việt**  
Định dạng chính: **Markdown (`.md`)**  
Cách quản lý khuyến nghị: **Git/GitHub/GitLab**

---

## 1. Tư duy chính

Template này không xem tài liệu requirement là file Word dài để lưu kho. Thay vào đó, requirement được quản lý như một phần của dự án:

- Có version bằng Git.
- Có mã requirement rõ ràng.
- Có backlog tổng.
- Có file chi tiết cho từng requirement.
- Có business rules tách riêng.
- Có stakeholder confirmation để chốt với khách/sếp.
- Có software design spec để dev/AI agent triển khai.
- Có change log để truy vết vì sao requirement thay đổi.

---

## 2. Cấu trúc folder

```text
docs/
  requirements/
    README.md
    backlog.md
    glossary.md
    stakeholder-decisions.md
    business-rules.md
    workflows.md
    data-model.md
    acceptance-criteria.md
    open-questions.md
    change-log.md
    reqs/
      HR-CONTRACT-001-tao-hop-dong-lao-dong.md
      HR-SALARY-001-lich-su-luong.md
      HR-BHXH-001-lich-su-bhxh.md

  specs/
    01-hr-contracts/
      software-design-spec.md
      implementation-plan.md
      test-cases.md
      validation-report.md
      proofs/
        README.md

  stakeholder/
    confirmations/
      2026-06-24-xac-nhan-yeu-cau-hop-dong-lao-dong.md

  ai/
    agent-guide.md
    coding-rules.md
    project-context.md

templates/
  requirement-item-template.md
  stakeholder-confirmation-template.md
  software-design-spec-template.md
  change-request-template.md
```

---

## 3. File nào là source of truth?

Source of truth chính nằm trong:

```text
docs/requirements/
```

Trong đó:

- `backlog.md`: danh sách tổng toàn bộ requirement.
- `reqs/*.md`: chi tiết từng requirement.
- `business-rules.md`: tập trung rule nghiệp vụ.
- `stakeholder-decisions.md`: các quyết định đã chốt.
- `change-log.md`: lịch sử thay đổi.

Không nên xem `stakeholder/confirmations` hoặc `specs` là source chính. Hai phần này là output được sinh/biên soạn từ source requirement.

---

## 4. Cách dùng đề xuất

### Bước 1: Ghi nhận yêu cầu thô

Cập nhật vào:

```text
docs/requirements/backlog.md
```

Trạng thái ban đầu thường là `Draft`.

### Bước 2: Viết chi tiết requirement

Tạo file trong:

```text
docs/requirements/reqs/
```

Ví dụ:

```text
HR-CONTRACT-001-tao-hop-dong-lao-dong.md
```

### Bước 3: Chốt với stakeholder

Tạo biên bản ở:

```text
docs/stakeholder/confirmations/
```

Sau khi chốt, cập nhật status requirement thành `Approved`.

### Bước 4: Viết spec cho dev/AI agent

Tạo/cập nhật file:

```text
docs/specs/01-hr-contracts/software-design-spec.md
```

Khi đủ rõ để làm, cập nhật status thành `Ready for Dev`.

### Bước 5: Sau khi code/test/UAT

Cập nhật:

```text
docs/requirements/change-log.md
docs/specs/01-hr-contracts/validation-report.md
```

Nếu có thay đổi requirement, quay lại cập nhật source trong `docs/requirements`.

---

## 5. Quy ước status

| Status | Ý nghĩa |
|---|---|
| Draft | Mới ghi nhận, chưa phân tích |
| In Review | Đang trao đổi/chờ xác nhận |
| Approved | Stakeholder đã chốt về nghiệp vụ |
| Ready for Dev | Đủ rõ để dev/AI agent triển khai |
| In Development | Đang triển khai |
| Ready for UAT | Sẵn sàng nghiệm thu |
| Done | Đã nghiệm thu/hoàn tất |
| Changed | Có thay đổi sau khi đã duyệt |
| Deprecated | Không còn dùng |

---

## 6. Quy ước mã requirement

Ví dụ:

```text
HR-CONTRACT-001
HR-SALARY-001
HR-BHXH-001
```

Cấu trúc:

```text
[DOMAIN]-[MODULE]-[NUMBER]
```

Ví dụ:

- `HR`: domain nhân sự
- `CONTRACT`: module hợp đồng
- `001`: số thứ tự

---

## 7. Cách làm việc với AI agent

Khi yêu cầu AI agent code, không prompt chung chung. Hãy trỏ AI đọc các file sau:

```text
docs/ai/project-context.md
docs/ai/coding-rules.md
docs/requirements/backlog.md
docs/requirements/reqs/HR-CONTRACT-001-tao-hop-dong-lao-dong.md
docs/specs/01-hr-contracts/software-design-spec.md
```

Prompt mẫu:

```text
Hãy đọc project-context, coding-rules, requirement HR-CONTRACT-001 và software-design-spec của module hr-contracts.
Sau đó lập implementation plan trước, chưa code ngay.
Nếu phát hiện thiếu rule hoặc mâu thuẫn, hãy ghi vào docs/requirements/open-questions.md.
```

---

## 8. Ghi chú

Template này là bản mẫu để bạn sửa theo từng dự án. Với dự án nhỏ, có thể dùng ít file hơn. Với dự án lớn, nên tách theo module/feature.
