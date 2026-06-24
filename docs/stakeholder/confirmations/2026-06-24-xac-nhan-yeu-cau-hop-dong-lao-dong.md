# Biên bản xác nhận yêu cầu phần mềm

## 1. Thông tin chung

| Nội dung | Giá trị |
|---|---|
| Dự án | HR Management System |
| Module | Quản lý hợp đồng lao động |
| Ngày trao đổi | 2026-06-24 |
| Người tham gia | Trưởng bộ phận HR, BA, Backend Developer |
| Người ghi nhận | BA |

## 2. Mục tiêu nghiệp vụ

Chuẩn hóa việc tạo và theo dõi hợp đồng lao động của nhân viên trên hệ thống, giảm thao tác thủ công và tạo nền tảng cho việc theo dõi lịch sử lương/BHXH.

## 3. Phạm vi đã thống nhất

- HR tạo được hợp đồng lao động cho nhân viên.
- Hệ thống kiểm tra mã hợp đồng không trùng.
- Một nhân viên chỉ có một hợp đồng đang hiệu lực.
- Hệ thống lưu loại hợp đồng, ngày bắt đầu, ngày kết thúc, lương cơ bản.
- Khi tạo hợp đồng có lương cơ bản hợp lệ, hệ thống tự tạo lịch sử lương.

## 4. Phạm vi chưa bao gồm trong giai đoạn này

- Ký số hợp đồng.
- Xuất file Word/PDF hợp đồng.
- Gửi email tự động cho nhân viên.
- Tích hợp phần mềm BHXH bên ngoài.
- Quy trình duyệt nhiều cấp.

## 5. Quy tắc nghiệp vụ đã chốt

| Mã | Nội dung | Ghi chú |
|---|---|---|
| BR-CONTRACT-001 | Một nhân viên chỉ được có một hợp đồng Active tại một thời điểm. | Áp dụng v1.0 |
| BR-CONTRACT-002 | Mã hợp đồng không được trùng. | Áp dụng v1.0 |
| BR-CONTRACT-004 | Hợp đồng thử việc không được vượt quá 2 tháng. | Áp dụng v1.0 |
| BR-SALARY-001 | Khi tạo hợp đồng có BaseSalary > 0, hệ thống tự tạo SalaryHistory. | Áp dụng v1.0 |

## 6. Các điểm còn chờ xác nhận

| ID | Nội dung | Người phụ trách | Hạn phản hồi |
|---|---|---|---|
| Q-CONTRACT-001 | Nếu nhân viên có hợp đồng Active cũ, có tự động expire hợp đồng cũ không? | HR | 2026-07-10 |
| Q-BHXH-001 | Lương đóng BHXH mặc định lấy từ BaseSalary hay nhập riêng? | HR | 2026-07-15 |

## 7. Điều kiện nghiệm thu giai đoạn v1.0

- HR tạo được hợp đồng hợp lệ cho nhân viên.
- Hệ thống không cho trùng mã hợp đồng.
- Hệ thống không cho nhân viên có hai hợp đồng Active.
- Hệ thống tự tạo lịch sử lương khi hợp đồng có BaseSalary hợp lệ.
- Dữ liệu hợp đồng hiển thị được trong hồ sơ nhân viên.

## 8. Kết luận

Các bên thống nhất sử dụng nội dung trên làm cơ sở phân tích, thiết kế và triển khai phần mềm cho module quản lý hợp đồng lao động giai đoạn v1.0.
