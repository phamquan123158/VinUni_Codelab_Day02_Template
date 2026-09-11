# 02 — Deep-Dive Report: Xanh SM hỗ trợ sự cố pin thấp

## Current-state workflow

1. Tài xế gọi hoặc chat báo pin thấp; điều phối viên tạo ticket (1 phút).
2. Điều phối viên xác minh biển số, GPS, % pin và loại xe (2 phút). **Handoff:** cuộc gọi/chat → ticket điều vận.
3. Điều phối viên tra dashboard trạm sạc tương thích và khả dụng (5 phút). **Bottleneck:** dữ liệu phân tán.
4. Điều phối viên soạn hướng dẫn đến trạm hoặc yêu cầu sạc di động (4 phút). **Bottleneck:** dễ diễn giải sai khi chịu áp lực thời gian.
5. Điều phối viên kiểm tra và gửi tin cho tài xế (2 phút).

Baseline giả định để lập kế hoạch là 14 phút/lượt; phải xác minh bằng log ticket ẩn danh trước pilot.

## Problem statement (6 fields)

| Field | Nội dung |
|---|---|
| Actor / Operator | Điều phối viên Xanh SM xử lý ticket pin thấp; tài xế nhận hướng dẫn. |
| Current workflow | Xác minh xe/GPS/pin, tra trạm, tạo hướng dẫn hoặc gọi đội sạc di động, sau đó duyệt và gửi. |
| Bottleneck | Tra cứu trạm tương thích/trống và biến dữ liệu kỹ thuật thành chỉ dẫn dễ hiểu. |
| Business impact | Xe chờ xử lý không thể phục vụ; điều phối viên mất công suất. Pilot đo thời gian xử lý, downtime và tỉ lệ route sai thay vì giả định doanh thu. |
| Success metric | P50 tạo draft dưới 3 phút; >=95% draft được chấp nhận hoặc chỉnh sửa nhẹ; 100% case pin `< 5%` sang mobile charger; 0 lần gửi tự động. |
| Operational boundary | AI chỉ đọc dữ liệu đã cấp quyền và tạo draft bắt đầu `[DRAFT_ONLY]`. Không tự gửi tin/đặt lịch/điều xe. Pin `< 5%` không được gợi ý trạm xa hơn 5 km; phải trả `dispatch_mobile_charger`. Dữ liệu thiếu, API lỗi hoặc schema sai → fallback thủ công. |

## AI fit & future-state flow

**Kiến trúc: Rule / State Machine + LLM Feature; không dùng agent tự trị.** Rule xử lý dữ kiện quyết định (ngưỡng pin, khoảng cách, quyền hành động); LLM chỉ tóm tắt input tự do và tạo JSON/tin nhắn nháp.

```text
Tài xế báo pin thấp
  → Rule xác minh ticket, GPS, % pin, loại xe
  → pin < 5%? ── Có → dispatch_mobile_charger
                 Không → lấy trạm từ API nội bộ
  → LLM tạo JSON + [DRAFT_ONLY] draft từ dữ liệu đã xác thực
  → Điều phối viên kiểm tra, phê duyệt và gửi
  → Audit log

Fallback: API thiếu dữ liệu / JSON lỗi / người duyệt từ chối
  → checklist và quy trình tra cứu–soạn tay hiện tại.
```

## Evaluation

| AI readiness item | Trạng thái | Hành động tiếp theo |
|---|---|---|
| Dữ liệu mẫu/log sạch | Chưa đủ | Ẩn danh tối thiểu 200 ticket, tạo GPS giả lập và snapshot trạng thái trạm. |
| Rủi ro có kiểm soát | Có | Rule cứng, HITL, audit log, schema validation và fallback thủ công. |
| Stakeholder sẵn sàng | Chưa xác nhận | Workshop với điều phối viên, sau đó chạy shadow mode. |

### Quyết định: NOT YET

Scope kỹ thuật phù hợp cho prototype, nhưng chưa có baseline đã xác minh, dữ liệu trạm thời gian thực đủ tin cậy và cam kết thay đổi quy trình. Nhóm sẽ chuyển sang **GO** khi đạt metric trong shadow mode, API ổn định và vận hành phê duyệt HITL.
