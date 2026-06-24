# Software Design Specification - HR Contracts

## 1. Related Requirements

- HR-CONTRACT-001 - Tạo hợp đồng lao động
- HR-SALARY-001 - Tự động tạo lịch sử lương khi có lương cơ bản

## 2. Objective

Thiết kế kỹ thuật cho module tạo hợp đồng lao động, bao gồm domain model, API contract, validation, business logic, error handling và test cases chính.

## 3. Existing System Context

> Đây là dữ liệu mẫu. Khi áp dụng dự án thật, cập nhật theo source code hiện tại.

- Backend: .NET 8 Web API
- Database: PostgreSQL
- Architecture: Clean Architecture + CQRS
- ORM: EF Core
- Pattern: Repository/Unit of Work nếu project hiện tại đang dùng
- Auth: JWT + Role-based permission

## 4. Domain Model

### Entity: EmployeeContract

| Field | Type | Required | Description |
|---|---|---|---|
| Id | Guid | Yes | Primary key |
| EmployeeId | Guid | Yes | FK to Employee |
| ContractCode | string | Yes | Mã hợp đồng, unique |
| ContractType | ContractType | Yes | Probation, OneYear, ThreeYear, Indefinite |
| StartDate | DateOnly | Yes | Ngày bắt đầu |
| EndDate | DateOnly? | No | Ngày kết thúc |
| BaseSalary | decimal | Yes | Lương cơ bản |
| Status | ContractStatus | Yes | Draft, Active, Expired, Terminated |
| CreatedAt | DateTimeOffset | Yes | Ngày tạo |
| UpdatedAt | DateTimeOffset? | No | Ngày cập nhật |

### Entity: SalaryHistory

| Field | Type | Required | Description |
|---|---|---|---|
| Id | Guid | Yes | Primary key |
| EmployeeId | Guid | Yes | FK to Employee |
| ContractId | Guid? | Yes if created from contract | FK to EmployeeContract |
| BaseSalary | decimal | Yes | Lương cơ bản |
| EffectiveDate | DateOnly | Yes | Ngày hiệu lực |
| SourceType | SalarySourceType | Yes | Contract, Appendix, ManualAdjustment |
| Note | string? | No | Ghi chú |

## 5. Enums

```csharp
public enum ContractType
{
    Probation = 1,
    OneYear = 2,
    ThreeYear = 3,
    Indefinite = 4
}

public enum ContractStatus
{
    Draft = 1,
    Active = 2,
    Expired = 3,
    Terminated = 4
}

public enum SalarySourceType
{
    Contract = 1,
    Appendix = 2,
    ManualAdjustment = 3
}
```

## 6. Business Logic

- Kiểm tra `EmployeeId` tồn tại.
- Kiểm tra `ContractCode` không trùng.
- Kiểm tra nhân viên chưa có hợp đồng `Active`.
- Kiểm tra `StartDate <= EndDate` nếu `EndDate` có giá trị.
- Nếu `ContractType = Probation`, thời hạn không được vượt quá 2 tháng.
- Nếu tạo hợp đồng thành công và `BaseSalary > 0`, tạo `SalaryHistory`.
- `SalaryHistory.EffectiveDate = EmployeeContract.StartDate`.
- `SalaryHistory.SourceType = Contract`.

## 7. API Contract

### POST `/api/employee-contracts`

#### Request

```json
{
  "employeeId": "11111111-1111-1111-1111-111111111111",
  "contractCode": "HDLD-2026-001",
  "contractType": "OneYear",
  "startDate": "2026-07-01",
  "endDate": "2027-06-30",
  "baseSalary": 9000000
}
```

#### Success Response

```json
{
  "id": "22222222-2222-2222-2222-222222222222",
  "employeeId": "11111111-1111-1111-1111-111111111111",
  "contractCode": "HDLD-2026-001",
  "status": "Active",
  "salaryHistoryCreated": true
}
```

#### Error Responses

| Case | HTTP Status | Message |
|---|---|---|
| Employee not found | 404 | Không tìm thấy nhân viên |
| Duplicate ContractCode | 400 | Mã hợp đồng đã tồn tại |
| Active contract exists | 400 | Nhân viên đã có hợp đồng đang hiệu lực |
| Invalid date range | 400 | Ngày kết thúc phải lớn hơn hoặc bằng ngày bắt đầu |
| Invalid probation duration | 400 | Hợp đồng thử việc không được vượt quá 2 tháng |

## 8. Permission

| Action | Role |
|---|---|
| Create Employee Contract | HR Admin |
| View Employee Contracts | HR Admin, Manager |
| Update Employee Contract | HR Admin |

## 9. Database/Migration Notes

- Tạo bảng `EmployeeContracts` nếu chưa tồn tại.
- Tạo bảng `SalaryHistories` nếu chưa tồn tại.
- Thêm unique index cho `EmployeeContracts.ContractCode`.
- Cân nhắc index cho `EmployeeContracts.EmployeeId` và `EmployeeContracts.Status`.
- Nếu dùng PostgreSQL, DateOnly cần mapping phù hợp với EF Core provider hiện tại.

## 10. Test Cases

| Test ID | Requirement | Nội dung |
|---|---|---|
| TC-CONTRACT-001 | HR-CONTRACT-001 | Tạo hợp đồng hợp lệ |
| TC-CONTRACT-002 | HR-CONTRACT-001 | Không cho trùng mã hợp đồng |
| TC-CONTRACT-003 | HR-CONTRACT-001 | Không cho tạo hai hợp đồng Active |
| TC-CONTRACT-004 | HR-CONTRACT-001 | Không cho StartDate > EndDate |
| TC-CONTRACT-005 | HR-CONTRACT-001 | Không cho hợp đồng thử việc vượt quá 2 tháng |
| TC-SALARY-001 | HR-SALARY-001 | Tạo SalaryHistory khi BaseSalary > 0 |

## 11. Implementation Notes for AI Agent

- Đọc `docs/ai/project-context.md` và `docs/ai/coding-rules.md` trước khi code.
- Không tự ý đổi kiến trúc hiện tại.
- Không tự ý đổi tên bảng/entity đã tồn tại nếu project thật đã có code cũ.
- Nếu phát hiện thiếu field hoặc mâu thuẫn rule, cập nhật `docs/requirements/open-questions.md` thay vì đoán.
- Sau khi triển khai, cập nhật `docs/specs/01-hr-contracts/validation-report.md`.
