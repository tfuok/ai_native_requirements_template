# Test Cases - HR Contracts

## TC-CONTRACT-001 - Tạo hợp đồng hợp lệ

| Field | Value |
|---|---|
| Requirement | HR-CONTRACT-001 |
| Preconditions | Employee tồn tại, chưa có hợp đồng Active |
| Input | ContractCode mới, ContractType OneYear, StartDate hợp lệ, EndDate hợp lệ, BaseSalary > 0 |
| Expected Result | Tạo hợp đồng status Active, trả về id hợp đồng |

## TC-CONTRACT-002 - Không cho trùng mã hợp đồng

| Field | Value |
|---|---|
| Requirement | HR-CONTRACT-001 |
| Preconditions | Đã tồn tại ContractCode `HDLD-2026-001` |
| Input | Tạo hợp đồng mới với ContractCode `HDLD-2026-001` |
| Expected Result | Trả lỗi `Mã hợp đồng đã tồn tại` |

## TC-CONTRACT-003 - Không cho tạo hai hợp đồng Active

| Field | Value |
|---|---|
| Requirement | HR-CONTRACT-001 |
| Preconditions | Employee đã có hợp đồng Active |
| Input | Tạo hợp đồng Active mới |
| Expected Result | Trả lỗi `Nhân viên đã có hợp đồng đang hiệu lực` |

## TC-CONTRACT-004 - Không cho StartDate > EndDate

| Field | Value |
|---|---|
| Requirement | HR-CONTRACT-001 |
| Input | StartDate = 2026-08-01, EndDate = 2026-07-01 |
| Expected Result | Trả lỗi `Ngày kết thúc phải lớn hơn hoặc bằng ngày bắt đầu` |

## TC-CONTRACT-005 - Không cho hợp đồng thử việc quá 2 tháng

| Field | Value |
|---|---|
| Requirement | HR-CONTRACT-001 |
| Input | ContractType = Probation, StartDate = 2026-07-01, EndDate = 2026-10-01 |
| Expected Result | Trả lỗi `Hợp đồng thử việc không được vượt quá 2 tháng` |

## TC-SALARY-001 - Tạo SalaryHistory khi BaseSalary hợp lệ

| Field | Value |
|---|---|
| Requirement | HR-SALARY-001 |
| Input | Tạo hợp đồng với BaseSalary = 9000000 |
| Expected Result | Tạo thêm SalaryHistory với BaseSalary = 9000000 và EffectiveDate = Contract.StartDate |
