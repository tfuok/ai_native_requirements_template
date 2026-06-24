# HR-SALARY-001 - Tự động tạo lịch sử lương khi có lương cơ bản

## 1. Metadata

| Field | Value |
|---|---|
| Status | Approved |
| Priority | Should |
| Type | Feature |
| Module | Salary |
| Owner | BA |
| Source | Internal Analysis |
| Created Date | 2026-06-24 |
| Last Updated | 2026-06-24 |

## 2. Problem

Khi lương cơ bản của nhân viên thay đổi theo hợp đồng hoặc phụ lục hợp đồng, HR cần có lịch sử lương để đối chiếu theo thời gian. Nếu chỉ lưu lương hiện tại trên hồ sơ nhân viên thì sẽ mất dấu các lần thay đổi trước đó.

## 3. Goal

Tự động tạo bản ghi lịch sử lương khi hợp đồng lao động được tạo với mức `BaseSalary` hợp lệ.

## 4. Users / Actors

- HR Admin
- System

## 5. Scope

### In Scope

- Tạo `SalaryHistory` khi tạo hợp đồng có `BaseSalary > 0`.
- Lưu ngày hiệu lực theo `StartDate` của hợp đồng.
- Gắn lịch sử lương với nhân viên và hợp đồng nguồn.

### Out of Scope

- Quy trình duyệt thay đổi lương.
- Tính lương hàng tháng.
- Tính thuế TNCN.

## 6. Main Workflow

1. System nhận yêu cầu tạo hợp đồng lao động.
2. Hợp đồng được validate thành công.
3. System kiểm tra `BaseSalary`.
4. Nếu `BaseSalary > 0`, System tạo `SalaryHistory`.
5. `EffectiveDate` của lịch sử lương bằng `StartDate` của hợp đồng.

## 7. Business Rules

| Rule ID | Rule | Required |
|---|---|---|
| BR-SALARY-001 | Khi tạo hợp đồng có `BaseSalary > 0`, tạo `SalaryHistory`. | Yes |
| BR-SALARY-002 | `EffectiveDate` của `SalaryHistory` lấy theo `StartDate` của hợp đồng. | Yes |
| BR-SALARY-003 | `SalaryHistory.SourceType = Contract` nếu phát sinh từ hợp đồng. | Yes |

## 8. Data Requirements

### SalaryHistory Fields

| Field | Type | Required | Note |
|---|---|---|---|
| Id | Guid | Yes | Primary key |
| EmployeeId | Guid | Yes | FK tới Employee |
| ContractId | Guid? | Yes | Hợp đồng nguồn |
| BaseSalary | decimal | Yes | Lương cơ bản |
| EffectiveDate | DateOnly | Yes | Ngày hiệu lực |
| SourceType | enum | Yes | Contract, Appendix, ManualAdjustment |
| Note | string? | No | Ghi chú |

## 9. Acceptance Criteria

### AC-001: Tạo lịch sử lương từ hợp đồng

Given HR tạo hợp đồng có `BaseSalary = 9000000`  
When hợp đồng được tạo thành công  
Then System tạo `SalaryHistory` với `BaseSalary = 9000000`

### AC-002: Không tạo lịch sử lương nếu lương không hợp lệ

Given HR tạo hợp đồng có `BaseSalary <= 0`  
When System validate dữ liệu  
Then System trả lỗi và không tạo hợp đồng/lịch sử lương

## 10. Open Questions

| ID | Question | Owner | Status |
|---|---|---|---|
| Q-SALARY-001 | Khi cập nhật hợp đồng thì có tự tạo lịch sử lương mới không? | HR | Open |

## 11. Change History

| Date | Change | Reason | By |
|---|---|---|---|
| 2026-06-24 | Tạo requirement ban đầu | Cần theo dõi lịch sử lương theo hợp đồng | BA |
