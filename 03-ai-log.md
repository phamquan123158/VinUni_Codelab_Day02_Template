# 03 — AI Log & Reflection

> ⚠️ **Lưu ý:** Đây là bản nháp phản ánh dựa trên phiên làm việc thực tế với Claude trong buổi
> lab này. Vì tiêu chí I3 yêu cầu "phản ánh trung thực" của cá nhân, hãy đọc lại và **chỉnh sửa
> theo đúng trải nghiệm thật của bạn** trước khi nộp — đặc biệt là những chỗ AI trả lời sai/chưa
> chuẩn mà chính bạn phát hiện ra.

---

## AI đã hỗ trợ tôi như thế nào?

Tôi dùng Claude làm "thought-partner" trong Phase 1 (SCAN) khi chưa nghĩ ra đủ 5 bài toán thực
tế. Tôi cho Claude đọc `README.md`, `01-worksheet.md`, `02-deliverable-example.md` và
`03-inspiration-kit.md`, sau đó nhờ brainstorm các pain point khác với ví dụ mẫu đã có sẵn (ví dụ
mẫu đã dùng case "Xanh SM xử lý sự cố sạc pin" và "Vinhomes CSKH", nên tôi yêu cầu ý tưởng không
trùng để nhóm có góc nhìn riêng).

Kết quả hữu ích:
- Claude liệt kê nhanh 5 bài toán trải đều across các công ty thành viên Vingroup theo đúng 4
  lenses của worksheet, giúp tôi có điểm khởi đầu thay vì nhìn trang giấy trắng.
- Khi tôi hỏi nên chọn bài toán nào để Deep-Dive, Claude đưa ra lập luận rõ ràng dựa trên các
  tiêu chí của Phase 5 (metric đo được, Operational Boundary khả thi, không cần kiến trúc phức
  tạp) — điều này giúp tôi hiểu rõ hơn *tại sao* một bài toán "AI Fit" tốt chứ không chỉ chọn đại.
- Claude giúp soạn khung Problem Statement 6-field và vẽ ASCII workflow theo đúng format worksheet
  yêu cầu, tiết kiệm thời gian trình bày để nhóm tập trung thảo luận nội dung.

## AI trả lời sai / hallucination ở đâu?

*(Phần này cần bạn tự kiểm chứng và điền số liệu thật — các con số dưới đây do Claude ước lượng
mang tính minh hoạ, KHÔNG có nguồn dữ liệu thật từ VinFast/Vin Smart Future):*

- Các con số như "300-400 cảnh báo/ngày", "40-50 giờ nhân lực/ngày", hay thời gian xử lý "8
  phút/cảnh báo" trong `02-deep-dive-report.md` là **ước lượng hợp lý do AI tự đặt ra** để minh
  hoạ cách viết Business Impact, không phải số liệu thật của VinFast. Nếu nộp bài, nhóm cần thay
  bằng số liệu ước tính có căn cứ hơn (hỏi giảng viên, tham khảo báo cáo công khai, hoặc ít nhất
  nêu rõ đây là giả định).
- Claude có xu hướng đưa ra giải pháp "an toàn" (LLM Feature + HITL) cho hầu hết bài toán — cần tự
  phản biện xem có phải lúc nào Rule-based đơn giản cũng không đủ, đúng như tinh thần "Problem
  First, AI Second" mà `03-inspiration-kit.md` nhấn mạnh.

## Tôi đã sửa prompt/ranh giới ra sao để đạt kết quả chuẩn?

- Tôi yêu cầu Claude tránh lặp lại nguyên văn case đã có trong `02-deliverable-example.md` để
  buộc nó đưa ra ý tưởng mới thay vì chỉ diễn giải lại ví dụ có sẵn.
- Khi nhờ viết `SYSTEM_PROMPT` cho `prompt_prototype.py`, tôi giữ nguyên đúng 2 quy tắc ranh giới
  đã được đề bài quy định cứng (`[DRAFT_ONLY]` và ngưỡng pin 5% → `dispatch_mobile_charger`) thay
  vì để AI tự sáng tạo ranh giới khác, vì autograder kiểm tra chính xác các từ khoá này.
- Trước khi nộp, tôi tự chạy lại `prompt_prototype.py` với `GEMINI_API_KEY` thật để xác nhận Rule
  1 và Rule 2 thực sự được giữ vững khi bị "tấn công" bằng prompt khẩn cấp, thay vì tin tưởng mù
  quáng rằng AI viết system prompt là đủ tốt.

## Bài học rút ra

AI là công cụ tăng tốc rất tốt cho việc *cấu trúc hoá* ý tưởng và tuân theo format có sẵn, nhưng
số liệu định lượng và quyết định GO/NOT YET/NO-GO cuối cùng vẫn cần con người kiểm chứng bằng dữ
liệu thật hoặc ít nhất là giả định được nêu rõ ràng, minh bạch.
