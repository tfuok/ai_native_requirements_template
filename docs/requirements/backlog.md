# Requirement Backlog

## Dự án mẫu

**HR Management System** - Module quản lý hợp đồng lao động, lịch sử lương và lịch sử BHXH.

## Quy ước trạng thái

| Status | Ý nghĩa |
|---|---|
| Draft | Mới ghi nhận, chưa phân tích |
| In Review | Đang trao đổi/chờ xác nhận |
| Approved | Stakeholder đã chốt nghiệp vụ |
| Ready for Dev | Đủ rõ để dev/AI agent triển khai |
| In Development | Đang triển khai |
| Ready for UAT | Sẵn sàng nghiệm thu |
| Done | Đã hoàn tất |
| Changed | Có thay đổi sau khi đã duyệt |
| Deprecated | Không còn dùng |

## Danh sách requirement

| Req ID | Title | Type | Module | Priority | Status | Owner | Source | Target Release | Detail |
|---|---|---|---|---|---|---|---|---|---|
| HR-CONTRACT-001 | Tạo hợp đồng lao động | Feature | Contract | Must | Ready for Dev | BA | HR Meeting 2026-06-24 | v1.0 | `./reqs/HR-CONTRACT-001-tao-hop-dong-lao-dong.md` |
| HR-SALARY-001 | Tự động tạo lịch sử lương khi có lương cơ bản | Feature | Salary | Should | Approved | BA | Internal Analysis | v1.0 | `./reqs/HR-SALARY-001-lich-su-luong.md` |
| HR-BHXH-001 | Tạo lịch sử BHXH từ mức lương đóng BHXH | Feature | Insurance | Should | Draft | BA | HR Request | v1.1 | `./reqs/HR-BHXH-001-lich-su-bhxh.md` |

## Release Mapping

| Release | Requirements | Ghi chú |
|---|---|---|
| v1.0 | HR-CONTRACT-001, HR-SALARY-001 | Ưu tiên để HR tạo và theo dõi hợp đồng/lương |
| v1.1 | HR-BHXH-001 | Tách phase sau do cần xác nhận thêm rule đóng BHXH |

## Definition of Ready for Dev

Một requirement được xem là `Ready for Dev` khi có đủ:

- Problem rõ.
- Goal rõ.
- Scope in/out rõ.
- Workflow chính.
- Business rules bắt buộc.
- Data impact.
- API/system impact nếu có.
- Acceptance criteria.
- Edge cases quan trọng.
- Không còn open question blocker.

## Definition of Done

Một requirement được xem là `Done` khi:

- Code đã merge.
- Test case chính đã pass.
- UAT được stakeholder xác nhận.
- Change log đã cập nhật.
- Tài liệu liên quan đã cập nhật nếu có thay đổi.
