# HR-BHXH-001 - Tạo lịch sử BHXH từ mức lương đóng BHXH

## 1. Metadata

| Field | Value |
|---|---|
| Status | Draft |
| Priority | Should |
| Type | Feature |
| Module | Insurance |
| Owner | BA |
| Source | HR Request |
| Created Date | 2026-06-24 |
| Last Updated | 2026-06-24 |

## 2. Problem

HR cần theo dõi mức lương đóng BHXH và lịch sử thay đổi theo từng nhân viên. Hiện tại thông tin này dễ bị lẫn với lương thực nhận hoặc lương cơ bản trong hợp đồng.

## 3. Goal

Cho phép hệ thống tạo lịch sử BHXH từ mức lương đóng BHXH và tỷ lệ cấu hình theo từng thời điểm.

## 4. Scope

### In Scope

- Ghi nhận mức lương đóng BHXH.
- Tạo lịch sử BHXH cho nhân viên.
- Lưu thời gian hiệu lực.

### Out of Scope

- Nộp hồ sơ BHXH điện tử.
- Kết nối cổng BHXH.
- Tự động cập nhật quy định pháp luật mới.

## 5. Draft Business Rules

| Rule ID | Rule | Status |
|---|---|---|
| BR-BHXH-001 | Lương đóng BHXH có thể khác lương cơ bản. | Draft |
| BR-BHXH-002 | Tỷ lệ đóng của nhân viên và công ty lấy từ cấu hình hệ thống. | Draft |
| BR-BHXH-003 | Khi mức đóng thay đổi, tạo bản ghi lịch sử mới thay vì ghi đè. | Draft |

## 6. Open Questions

| ID | Question | Owner | Status |
|---|---|---|---|
| Q-BHXH-001 | Mức lương đóng BHXH mặc định lấy từ BaseSalary hay nhập riêng? | HR | Open |
| Q-BHXH-002 | Có cần lưu tỷ lệ đóng của công ty và nhân viên tại thời điểm tạo lịch sử không? | HR | Open |
| Q-BHXH-003 | Có cần báo cáo tổng tiền đóng theo tháng không? | HR | Open |

## 7. Change History

| Date | Change | Reason | By |
|---|---|---|---|
| 2026-06-24 | Tạo draft requirement | HR đề xuất theo dõi BHXH | BA |
