# TEAM — Day04, K4-L3B

**Làm cá nhân.** Mỗi người tự viết và commit phần INDIVIDUAL của mình.

## Thông tin bài nộp

- Tên nhóm: Trần Xuân Tùng (Cá nhân)
- Người đại diện / MSSV: Trần Xuân Tùng / 2A202602787
- Tên repo: `K4-L3-DAY04-TranXuanTung-2A202602787-PromptEngineeringToolCalling`
- URL repo, nhánh nộp, commit chốt: `https://github.com/xuantungtran64-ai/K4-L3-DAY04-TranXuanTung-2A202602787-PromptEngineeringToolCalling.git`, nhánh `main`, commit chốt: `311580e2b12f92fcd747b3533764be6ae5aaa847`
- Deadline áp dụng và link thông báo đổi hạn nếu có: 23:59 ngày làm lab, Asia/Ho_Chi_Minh (UTC+07:00)

## Thành viên

| Họ và tên | MSSV | GitHub | Vai trò và công việc | File/commit/PR |
|---|---|---|---|---|
| Trần Xuân Tùng | 2A202602787 | xuantungtran64-ai | Toàn bộ dự án: Cấu hình môi trường, thiết kế Prompt & Tools, thực nghiệm v0–v3, viết 10 test cases, hoàn thiện REPORT và TEAM | `system_prompt.md`, `tools.yaml`, `version_log.csv`, `eval_group.json`, `REPORT.md`, `TEAM.md` |

## Nhận xét chung

- Kết quả và bằng chứng: Trợ lý IT Helpdesk đã phân luồng chính xác các nhóm công cụ tra cứu dịch vụ dùng chung (`check_service_status`), kiểm tra thiết bị cụ thể (`inspect_device`), tra cứu hướng dẫn cẩm nang (`search_kb`) và danh bạ nhân viên (`lookup_user`). Có cơ chế dừng lại hỏi xác nhận rõ ràng trước khi tạo ticket (`create_ticket`), không tự đoán `asset_id` hay `employee_id` khi thiếu thông tin. Bằng chứng được lưu trữ chi tiết trong `starter_v0/runs/` và `starter_v0/artifacts/version_log.csv`.
- Thay đổi hiệu quả nhất: Ràng buộc quy tắc ranh giới xác nhận (confirmation boundary) với tool `clarify` khi người dùng yêu cầu tạo ticket, đồng thời bổ sung mô tả phạm vi chi tiết cho từng công cụ trong `tools.yaml`.
- Giới hạn còn lại: Khi người dùng đưa ra câu hỏi phức tạp kết hợp nhiều dịch vụ cùng lúc, agent ưu tiên xử lý tác vụ chính đầu tiên thay vì gọi song song nhiều công cụ độc lập.
- Cách phân công và tích hợp: Làm cá nhân; thực hiện theo quy trình chuẩn của bài lab: thiết lập baseline v0 \(\to\) Giả thuyết 1 (khắc phục nhầm lẫn công cụ) \(\to\) Giả thuyết 2 (xử lý thiếu thông tin và out-of-scope) \(\to\) Giả thuyết 3 (xác nhận trước khi tạo ticket và bảo vệ dữ liệu nội bộ).

## INDIVIDUAL

### Trần Xuân Tùng — 2A202602787

- Phần việc và file/commit/PR: Thiết lập môi trường chạy với provider Gemini (`gemini-2.5-flash`), bổ sung xử lý rate-limit và retry trong `gemini_provider.py`; tinh chỉnh `starter_v0/artifacts/system_prompt.md` và `starter_v0/artifacts/tools.yaml` qua các phiên bản v0, v1, v2, v3; soạn 10 test cases trong `starter_v0/data/eval_group.json`; hoàn thiện `starter_v0/artifacts/REPORT.md`, `version_log.csv` và `TEAM.md`.
- Quyết định, khó khăn và cách xử lý: Khó khăn lớn nhất là gặp lỗi rate-limit 429 và 503 từ API do model mặc định thử nghiệm `gemini-3.5-flash` bị hạn chế 20 requests/ngày; đã quyết định chuyển sang model tiêu chuẩn `gemini-2.5-flash` và thiết lập giãn cách 2 giây cùng exponential backoff. Về mặt prompt engineering, mô hình ban đầu thường tự ý gọi `create_ticket` khi chưa có xác nhận; đã xử lý triệt để bằng cách thiết lập quy tắc bắt buộc dừng lại và gọi `clarify` (`response_type="yes_no"`) để xin xác nhận trước.
- Điều đã học: Nắm vững cơ chế Tool Calling / Function Calling có cấu trúc; kỹ năng viết mô tả schema chuẩn xác để định hướng LLM ra quyết định chính xác; cách phòng chống rò rỉ dữ liệu nội bộ ra công cụ tìm kiếm bên ngoài.
- AI/công cụ đã dùng và cách kiểm tra: Sử dụng Gemini API, Python venv, Antigravity AI assistant để hỗ trợ phân tích log và kiểm tra tính hợp lệ của schema; tự kiểm tra bằng cách kiểm tra trực tiếp từng kết quả trong các file JSON run và đối chiếu với tiêu chí rubric.
- Thời điểm đã tự nộp URL repo chung trên VLearn: 23:00 16/09/2026
