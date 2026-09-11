# 01 — Problem Scan & Quick Assess

## Phase 1 — Scan cơ hội

| # | Công ty | Lens | Bài toán / bottleneck |
|---|---|---|---|
| 1 | Xanh SM | Tốn thời gian | Khi tài xế báo pin thấp, điều phối viên phải kiểm tra xe, GPS, % pin, loại xe và trạm phù hợp trước khi tạo hướng dẫn. |
| 2 | VinFast | Lặp lại | Đối soát phiên sạc, hóa đơn và chênh lệch dữ liệu giữa xe, trạm sạc và đối tác. |
| 3 | Vinhomes | AI-upgrade | Phân loại và định tuyến phản ánh cư dân từ nhiều kênh đến đúng đội phụ trách. |
| 4 | Vinmec | Tốn thời gian | Tổng hợp ghi chú điều trị thành bản tóm tắt xuất viện dễ hiểu cho bệnh nhân. |
| 5 | Vinpearl / VinWonders | Pain từ người khác | Trả lời lặp lại các câu hỏi về vé, giờ mở cửa và chính sách đổi lịch trước chuyến đi. |

## Phase 2 — Quick Problem Cards

### Card 1 — Xanh SM: hỗ trợ sự cố pin thấp

| Mục | Nội dung |
|---|---|
| Actor | Tài xế Xanh SM và điều phối viên trung tâm vận hành. |
| Workflow hiện tại | Tài xế báo sự cố → xác minh xe/GPS/% pin → tra trạng thái trạm phù hợp → soạn hướng dẫn hoặc gọi sạc di động → điều phối viên duyệt/gửi. |
| Bottleneck | Tra cứu dữ liệu rải ở nhiều màn hình và chuyển thông tin kỹ thuật thành hướng dẫn rõ ràng; baseline giả định 8–10 phút/lượt cho hai bước này. |
| AI hỗ trợ | Rule xử lý ngưỡng pin/khoảng cách; LLM tóm tắt báo cáo và tạo bản nháp. |
| Metric | P50 tạo draft dưới 3 phút; 100% case pin `< 5%` sang mobile charger; 0 tin tự gửi không duyệt. |
| Architecture | **Rule / State Machine + LLM Feature**. |

### Card 2 — Vinhomes: phân loại khiếu nại cư dân

| Mục | Nội dung |
|---|---|
| Actor | Nhân viên CSKH, ban quản lý tòa nhà và cư dân. |
| Workflow hiện tại | Nhận ticket → đọc nội dung/ảnh → chọn nhóm vấn đề → chuyển đội xử lý → soạn phản hồi. |
| Bottleneck | Nội dung tự do có thể chứa nhiều vấn đề; dễ chuyển sai nhóm xử lý. |
| AI hỗ trợ | LLM trích xuất chủ đề/mức khẩn cấp và tạo draft; rule chuyển sự cố nguy hiểm sang hotline. |
| Metric | 85% ticket được gợi ý đúng nhóm trong dưới 30 giây; giảm 30% chuyển sai; mọi phản hồi cần người duyệt. |
| Architecture | **Rule + LLM Feature**. |

### Card 3 — Vinpearl / VinWonders: trợ lý thông tin trước chuyến đi

| Mục | Nội dung |
|---|---|
| Actor | Khách và nhân viên CSKH. |
| Workflow hiện tại | Khách nhắn/gọi → nhân viên tra giá/chính sách → trả lời → chuyển cấp nếu có đổi hoặc hoàn tiền. |
| Bottleneck | Chính sách thay đổi theo địa điểm, ngày và loại vé; nhân viên phải tra cứu lặp lại. |
| AI hỗ trợ | RAG từ knowledge base đã duyệt để trả lời FAQ đa ngôn ngữ; không tự đổi vé hoặc hoàn tiền. |
| Metric | 70% FAQ được tự phục vụ; QA lấy mẫu đạt ít nhất 95% chính xác; CSAT không giảm. |
| Architecture | **LLM Feature (RAG)**. |

## Bài toán được chọn

Nhóm chọn **Card 1 — hỗ trợ sự cố pin thấp cho Xanh SM**. Đây là luồng có tác động vận hành rõ và ranh giới an toàn có thể mã hóa bằng rule. LLM chỉ tạo draft, nên không được trao quyền điều phối hay gửi tin độc lập.
