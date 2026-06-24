# Business Rules

File này tập trung toàn bộ rule nghiệp vụ quan trọng của dự án.  
Mỗi rule nên có mã riêng để trace sang requirement, spec, test case và UAT.

## Contract Rules

| Rule ID | Nội dung | Requirement | Status |
|---|---|---|---|
| BR-CONTRACT-001 | Một nhân viên chỉ được có một hợp đồng `Active` tại một thời điểm. | HR-CONTRACT-001 | Approved |
| BR-CONTRACT-002 | `ContractCode` không được trùng trong hệ thống. | HR-CONTRACT-001 | Approved |
| BR-CONTRACT-003 | `StartDate` phải nhỏ hơn hoặc bằng `EndDate` nếu `EndDate` có giá trị. | HR-CONTRACT-001 | Approved |
| BR-CONTRACT-004 | Hợp đồng thử việc không được vượt quá 2 tháng. | HR-CONTRACT-001 | Approved |

## Salary Rules

| Rule ID | Nội dung | Requirement | Status |
|---|---|---|---|
| BR-SALARY-001 | Khi tạo hợp đồng có `BaseSalary > 0`, System phải tạo bản ghi `SalaryHistory`. | HR-SALARY-001 | Approved |
| BR-SALARY-002 | `EffectiveDate` của `SalaryHistory` lấy theo `StartDate` của hợp đồng. | HR-SALARY-001 | Approved |
| BR-SALARY-003 | `SalaryHistory.SourceType = Contract` nếu phát sinh từ hợp đồng. | HR-SALARY-001 | Approved |

## Insurance Rules

| Rule ID | Nội dung | Requirement | Status |
|---|---|---|---|
| BR-BHXH-001 | Lương đóng BHXH có thể khác lương cơ bản. | HR-BHXH-001 | Draft |
| BR-BHXH-002 | Tỷ lệ đóng của nhân viên và công ty lấy từ cấu hình hệ thống. | HR-BHXH-001 | Draft |
| BR-BHXH-003 | Khi mức đóng thay đổi, tạo bản ghi lịch sử mới thay vì ghi đè. | HR-BHXH-001 | Draft |
