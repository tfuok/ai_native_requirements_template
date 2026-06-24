# Requirements Source of Truth

Folder này là **nguồn sự thật chính** của requirement dự án.

Tất cả yêu cầu, rule nghiệp vụ, quyết định stakeholder, câu hỏi mở và lịch sử thay đổi phải được cập nhật tại đây trước khi sinh ra tài liệu cho stakeholder hoặc spec cho dev/AI.

## File chính

| File | Vai trò |
|---|---|
| `backlog.md` | Danh sách tổng tất cả requirement |
| `reqs/*.md` | Chi tiết từng requirement |
| `business-rules.md` | Tập trung toàn bộ rule nghiệp vụ |
| `workflows.md` | Mô tả luồng nghiệp vụ chính |
| `data-model.md` | Mô tả entity, field, relationship |
| `acceptance-criteria.md` | Tổng hợp điều kiện nghiệm thu |
| `stakeholder-decisions.md` | Các quyết định đã chốt với stakeholder |
| `open-questions.md` | Các điểm còn thiếu/chưa rõ |
| `change-log.md` | Lịch sử thay đổi requirement |

## Nguyên tắc

1. Mỗi requirement phải có `Req ID` duy nhất.
2. Mỗi thay đổi quan trọng phải cập nhật `change-log.md`.
3. Mỗi rule nghiệp vụ quan trọng phải có mã `BR-*`.
4. Không triển khai dev nếu requirement chưa đạt `Ready for Dev`, trừ khi team chủ động chấp nhận rủi ro.
5. Nếu stakeholder đổi ý, tạo change log và cập nhật requirement gốc.
