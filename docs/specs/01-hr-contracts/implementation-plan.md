# Implementation Plan - HR Contracts

## 1. Mục tiêu

Triển khai chức năng tạo hợp đồng lao động và tự động tạo lịch sử lương khi có BaseSalary hợp lệ.

## 2. Phạm vi triển khai

- Entity `EmployeeContract`.
- Entity `SalaryHistory` nếu chưa có.
- API tạo hợp đồng lao động.
- Validation theo business rules.
- Unit/integration test cơ bản.

## 3. Các bước thực hiện đề xuất

### Step 1: Kiểm tra code hiện tại

- Tìm entity `Employee`, `EmployeeContract`, `SalaryHistory` đã tồn tại chưa.
- Kiểm tra convention đặt tên folder, namespace, CQRS command/query.
- Kiểm tra cách project xử lý response/error hiện tại.

### Step 2: Cập nhật domain model

- Thêm/cập nhật entity `EmployeeContract`.
- Thêm/cập nhật entity `SalaryHistory`.
- Thêm enum `ContractType`, `ContractStatus`, `SalarySourceType` nếu chưa có.

### Step 3: Cập nhật database

- Tạo migration.
- Thêm unique index cho `ContractCode`.
- Thêm index theo `EmployeeId`, `Status`.

### Step 4: Tạo command/API

- `CreateEmployeeContractCommand`
- `CreateEmployeeContractCommandHandler`
- `CreateEmployeeContractRequest`
- `CreateEmployeeContractResponse`
- Endpoint `POST /api/employee-contracts`

### Step 5: Validation

- Employee tồn tại.
- ContractCode không trùng.
- Không có hợp đồng Active khác.
- Date hợp lệ.
- Probation không quá 2 tháng.
- BaseSalary > 0.

### Step 6: Tạo SalaryHistory

- Sau khi tạo hợp đồng thành công.
- Dùng chung transaction với tạo hợp đồng.
- Nếu tạo SalaryHistory lỗi thì rollback hợp đồng.

### Step 7: Test

- Test happy path.
- Test duplicate contract code.
- Test active contract exists.
- Test invalid date.
- Test probation duration.
- Test salary history created.

## 4. Rủi ro kỹ thuật

| Rủi ro | Cách xử lý |
|---|---|
| Project đã có entity tương tự nhưng tên khác | Không tạo trùng, mapping lại theo code hiện có |
| DateOnly mapping lỗi với PostgreSQL | Kiểm tra version EF Core/Npgsql |
| Business rule hợp đồng Active chưa chốt đầy đủ | Ghi vào open-questions.md |
| Transaction tạo hợp đồng + salary history chưa có pattern chuẩn | Theo UnitOfWork hiện tại nếu có |
