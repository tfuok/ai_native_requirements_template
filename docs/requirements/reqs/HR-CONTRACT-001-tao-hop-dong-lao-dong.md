# HR-CONTRACT-001 - Tạo hợp đồng lao động

## 1. Metadata

| Field | Value |
|---|---|
| Status | Ready for Dev |
| Priority | Must |
| Type | Feature |
| Module | Contract |
| Owner | BA |
| Source | HR Meeting 2026-06-24 |
| Created Date | 2026-06-24 |
| Last Updated | 2026-06-24 |

## 2. Problem

HR hiện đang quản lý hợp đồng lao động bằng file rời và thao tác thủ công. Việc này gây khó khăn khi cần biết nhân viên đang có hợp đồng nào còn hiệu lực, hợp đồng nào sắp hết hạn, và lịch sử lương/BHXH đã thay đổi ra sao theo từng thời điểm.

## 3. Goal

Cho phép HR tạo hợp đồng lao động cho nhân viên trong hệ thống, đồng thời làm nền cho các nghiệp vụ liên quan như lịch sử lương và lịch sử BHXH.

## 4. Users / Actors

- HR Admin
- System
- Employee

## 5. Scope

### In Scope

- Tạo hợp đồng lao động mới cho nhân viên.
- Ghi nhận loại hợp đồng, mã hợp đồng, ngày bắt đầu, ngày kết thúc, lương cơ bản.
- Validate dữ liệu hợp đồng.
- Gắn hợp đồng với nhân viên.
- Đánh dấu trạng thái hợp đồng là `Active` khi hợp đồng có hiệu lực.
- Tự động tạo lịch sử lương nếu có `BaseSalary` hợp lệ.

### Out of Scope

- Ký số hợp đồng.
- Gửi email tự động cho nhân viên.
- Tự động sinh file Word/PDF hợp đồng.
- Tích hợp phần mềm BHXH bên ngoài.
- Quy trình duyệt nhiều cấp.

## 6. Main Workflow

1. HR Admin vào hồ sơ nhân viên.
2. HR Admin chọn chức năng tạo hợp đồng lao động.
3. HR Admin nhập thông tin hợp đồng.
4. System validate dữ liệu đầu vào.
5. System kiểm tra nhân viên có hợp đồng `Active` hay chưa.
6. Nếu hợp lệ, System tạo hợp đồng mới với trạng thái `Active`.
7. Nếu có `BaseSalary > 0`, System tạo bản ghi `SalaryHistory`.
8. System trả kết quả tạo hợp đồng thành công.

## 7. Business Rules

| Rule ID | Rule | Required |
|---|---|---|
| BR-CONTRACT-001 | Một nhân viên chỉ được có một hợp đồng `Active` tại một thời điểm. | Yes |
| BR-CONTRACT-002 | `ContractCode` không được trùng trong hệ thống. | Yes |
| BR-CONTRACT-003 | `StartDate` phải nhỏ hơn hoặc bằng `EndDate` nếu `EndDate` có giá trị. | Yes |
| BR-CONTRACT-004 | Hợp đồng thử việc không được vượt quá 2 tháng. | Yes |
| BR-SALARY-001 | Khi tạo hợp đồng có `BaseSalary > 0`, System phải tạo bản ghi `SalaryHistory`. | Yes |

## 8. Data Requirements

### Entity Impact

- Employee
- EmployeeContract
- SalaryHistory

### EmployeeContract Fields

| Field | Type | Required | Note |
|---|---|---|---|
| Id | Guid | Yes | Primary key |
| EmployeeId | Guid | Yes | FK tới Employee |
| ContractCode | string | Yes | Mã hợp đồng, unique |
| ContractType | enum | Yes | Probation, OneYear, ThreeYear, Indefinite |
| StartDate | DateOnly | Yes | Ngày bắt đầu |
| EndDate | DateOnly? | No | Ngày kết thúc, null nếu không xác định thời hạn |
| BaseSalary | decimal | Yes | Lương cơ bản tại thời điểm tạo hợp đồng |
| Status | enum | Yes | Draft, Active, Expired, Terminated |
| CreatedAt | DateTimeOffset | Yes | Thời điểm tạo |
| UpdatedAt | DateTimeOffset? | No | Thời điểm cập nhật gần nhất |

## 9. API/System Impact

| Method | Endpoint | Purpose |
|---|---|---|
| POST | `/api/employee-contracts` | Tạo hợp đồng lao động |
| GET | `/api/employees/{employeeId}/contracts` | Lấy danh sách hợp đồng của nhân viên |
| GET | `/api/employee-contracts/{id}` | Lấy chi tiết hợp đồng |

## 10. Acceptance Criteria

### AC-001: Tạo hợp đồng hợp lệ

Given nhân viên tồn tại và chưa có hợp đồng `Active`  
When HR Admin tạo hợp đồng với dữ liệu hợp lệ  
Then System tạo hợp đồng với trạng thái `Active`

### AC-002: Không cho trùng mã hợp đồng

Given đã tồn tại hợp đồng có `ContractCode = HDLD-001`  
When HR Admin tạo hợp đồng mới với `ContractCode = HDLD-001`  
Then System trả lỗi `Mã hợp đồng đã tồn tại`

### AC-003: Không cho tạo hai hợp đồng active

Given nhân viên đã có hợp đồng `Active`  
When HR Admin tạo thêm hợp đồng `Active` mới  
Then System trả lỗi `Nhân viên đã có hợp đồng đang hiệu lực`

### AC-004: Tự động tạo lịch sử lương

Given hợp đồng được tạo có `BaseSalary = 9000000`  
When System tạo hợp đồng thành công  
Then System tạo một bản ghi `SalaryHistory` tương ứng

## 11. Edge Cases

- Nhân viên không tồn tại.
- Nhân viên đã có hợp đồng `Active`.
- `ContractCode` bị trùng.
- `StartDate` lớn hơn `EndDate`.
- Hợp đồng thử việc vượt quá 2 tháng.
- `BaseSalary` bằng 0 hoặc âm.
- Hợp đồng không xác định thời hạn không có `EndDate`.

## 12. Stakeholder Confirmation

| Field | Value |
|---|---|
| Confirmed By | Trưởng bộ phận HR |
| Confirmed Date | 2026-06-24 |
| Confirmation Source | Biên bản xác nhận yêu cầu phần mềm |
| Note | Đã thống nhất phase 1 chưa bao gồm ký số và xuất file hợp đồng |

## 13. Open Questions

| ID | Question | Owner | Status |
|---|---|---|---|
| Q-CONTRACT-001 | Nếu nhân viên có hợp đồng Active cũ, có cho phép tự động expire hợp đồng cũ không? | HR | Deferred |

## 14. Change History

| Date | Change | Reason | By |
|---|---|---|---|
| 2026-06-24 | Tạo requirement ban đầu | HR cần quản lý hợp đồng trên hệ thống | BA |
| 2026-06-24 | Chốt phase 1 chưa bao gồm ký số/xuất file | Giảm phạm vi triển khai v1.0 | BA + HR |
