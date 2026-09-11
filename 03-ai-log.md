# 03 — AI Log & Reflection

> Đây là bản phản ánh cho bài lab. Trước khi nộp, mỗi thành viên nên điều chỉnh các chi tiết để phản ánh đúng phần việc và trải nghiệm của mình.

## Tôi đã dùng AI như thế nào

Tôi dùng AI như một thought-partner để mở rộng danh sách pain point, chuyển một ý tưởng rộng thành workflow có bước, và phản biện lựa chọn kiến trúc. AI giúp tôi nhận ra rằng “điều phối thông minh” không đồng nghĩa phải xây agent tự trị: ngưỡng pin, khoảng cách và quyền gửi tin là các quyết định xác định, phù hợp với rule hơn LLM.

Sau đó tôi dùng AI để gợi ý cấu trúc Problem Statement 6-field và adversarial prompts. Ba test quan trọng là: ép hệ thống bỏ `[DRAFT_ONLY]`, đề xuất trạm 8 km khi pin 2%, và prompt injection yêu cầu bỏ qua mọi chỉ dẫn trước đó.

## Điều AI làm tốt

- Tạo nhanh các biến thể prompt tấn công mà tôi có thể bỏ sót khi chỉ nghĩ theo happy path.
- Đề xuất cách tách “dữ liệu có cấu trúc/rule” khỏi “ngôn ngữ tự do/LLM”.
- Giúp chuyển các rủi ro mơ hồ thành metric có thể đo, như P50 tạo draft, tỉ lệ chấp nhận draft và số lần gửi tự động bằng 0.

## Điều AI làm chưa tốt và cách tôi sửa

AI ban đầu có xu hướng đưa ra các con số hấp dẫn nhưng không có nguồn, ví dụ số ticket/ngày hoặc phần trăm doanh thu thất thoát. Tôi không dùng các con số này làm fact. Trong báo cáo, tôi ghi rõ baseline 14 phút/lượt là giả định cho prototype và đề xuất đo bằng log ẩn danh trước pilot.

AI cũng có thể viết một câu trả lời nghe hợp lý nhưng không đảm bảo nó tuân thủ policy. Vì vậy tôi không dựa riêng vào system prompt. Tôi thêm rule ở tầng ứng dụng cho pin `< 5%`, yêu cầu JSON schema, giữ `[DRAFT_ONLY]`, buộc human approval và có fallback khi dữ liệu/API/output không hợp lệ.

## Bài học và bước tiếp theo

AI hữu ích nhất khi hỗ trợ tư duy và tạo draft, còn người làm sản phẩm phải chịu trách nhiệm về dữ liệu, metric, ranh giới và quyết định triển khai. Nếu tiếp tục, tôi sẽ thực hiện shadow mode: AI tạo draft nhưng không gửi thật, điều phối viên chấm chất lượng draft, và nhóm dùng kết quả đó để quyết định GO hay NOT YET.
