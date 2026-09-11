# 01 — Problem Scan & Quick Cards

> Nhóm: Vin Smart Future — Lab 02 AI Product Scoping
> Mảng lựa chọn để Deep-Dive: **VinFast — Ưu tiên hoá cảnh báo bảo trì pin (Predictive Maintenance Triage)**

---

# 🔍 Phase 1 — SCAN

| # | Subsidiary | Lens | Mô tả ngắn bài toán |
|---|------------|------|----------------------|
| 1 | **VinFast** | AI có thể tốt hơn | Trung tâm dịch vụ nhận hàng trăm cảnh báo telemetry pin/động cơ mỗi ngày, kỹ thuật viên phải tự đọc log để xếp ưu tiên xe nào cần triệu hồi gấp. |
| 2 | **Xanh SM** | Pain từ người khác | Tài xế phàn nàn hệ thống gợi ý điểm đón/trả khách sai vị trí thực tế (cổng phụ, tầng hầm), gây trễ chuyến và huỷ cuốc. |
| 3 | **Vinmec** | Tốn thời gian | Điều dưỡng tiếp nhận phải tự đọc mô tả triệu chứng để ước tính mức độ ưu tiên cấp cứu (triage) trước khi bác sĩ khám. |
| 4 | **Vinpearl** | Lặp lại | Bộ phận buồng phòng nhận yêu cầu dọn phòng/đổi phòng qua nhiều kênh (lễ tân, app, điện thoại) rồi tự tổng hợp thủ công thành lịch phân công. |
| 5 | **Vinhomes** | AI có thể tốt hơn | Ban quản lý tòa nhà mất nhiều giờ soạn thông báo cư dân (bảo trì, cắt điện, sự kiện) bằng tay cho từng tòa, thiếu nhất quán văn phong. |

---

# 🃏 Phase 2 — QUICK-ASSESS

## Quick Problem Card #1 — VinFast: Ưu tiên hoá cảnh báo bảo trì pin ⭐ (Chọn Deep-Dive)

```
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #1                                        │
│                                                               │
│ Bài toán: Kỹ thuật viên trung tâm dịch vụ VinFast phải tự đọc │
│ hàng trăm log cảnh báo telemetry pin/động cơ mỗi ngày để xác  │
│ định xe nào cần triệu hồi/kiểm tra khẩn cấp.                  │
│ Công ty thành viên: [x] VinFast                               │
│                                                               │
│ Ai đang đau (Actor)? Kỹ thuật viên trung tâm dịch vụ          │
│                                                               │
│ Workflow thủ công hiện tại (4 bước):                          │
│   1. Nhận log cảnh báo ──> 2. Đọc & phân loại thủ công        │
│   ──> 3. Tra cứu lịch sử xe ──> 4. Xếp lịch kiểm tra ưu tiên  │
│                                                               │
│ Bước nào tốn thời gian/lỗi nhất? Bước 2-3 (⏱ ~8 phút/cảnh báo)│
│ AI có thể nhảy vào hỗ trợ ở bước nào? Bước 2-3 (tóm tắt log,  │
│ đối chiếu ngưỡng an toàn, giải thích mức độ nghiêm trọng)     │
│                                                               │
│ Đo thành công bằng gì (Metric có số)?                         │
│   "Giảm thời gian rà soát cảnh báo từ 8 phút ──> dưới 2 phút, │
│    giảm tỉ lệ bỏ sót cảnh báo nghiêm trọng về 0%"             │
│                                                               │
│ Quick Architecture: [ ] No AI  [x] LLM  [ ] Agent (kèm Rule   │
│ cứng cho ngưỡng an toàn nhiệt độ/điện áp pin)                 │
└─────────────────────────────────────────────────────────────┘
```

## Quick Problem Card #2 — Xanh SM: Trợ lý mô tả điểm đón/trả chính xác

```
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #2                                        │
│                                                               │
│ Bài toán: Tài xế Xanh SM nhận toạ độ GPS không khớp lối vào   │
│ thực tế (cổng phụ, tầng hầm), phải gọi hỏi lại khách hoặc     │
│ tổng đài, gây trễ chuyến.                                     │
│ Công ty thành viên: [x] Xanh SM (GSM)                         │
│                                                               │
│ Ai đang đau (Actor)? Tài xế + tổng đài hỗ trợ                 │
│                                                               │
│ Workflow thủ công hiện tại (3 bước):                          │
│   1. Tài xế đến toạ độ GPS ──> 2. Không tìm thấy lối vào,     │
│   gọi tổng đài/khách ──> 3. Tổng đài tra cứu, hướng dẫn lại   │
│                                                               │
│ Bước nào tốn thời gian/lỗi nhất? Bước 2 (⏱ 3-5 phút/lượt)     │
│ AI có thể nhảy vào hỗ trợ ở bước nào? Bước 1 (tổng hợp ghi    │
│ chú khách hàng cũ + landmark để draft chỉ dẫn trước)          │
│                                                               │
│ Đo thành công bằng gì (Metric có số)?                         │
│   "Giảm số cuộc gọi hỏi lại vị trí từ 30% ──> dưới 10% số     │
│    chuyến"                                                    │
│                                                               │
│ Quick Architecture: [ ] No AI  [x] LLM  [ ] Agent             │
└─────────────────────────────────────────────────────────────┘
```

## Quick Problem Card #3 — Vinmec: Hỗ trợ triage ban đầu

```
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #3                                        │
│                                                               │
│ Bài toán: Điều dưỡng tiếp nhận tự đọc mô tả triệu chứng bệnh  │
│ nhân để ước tính mức độ ưu tiên khám, dễ chậm khi đông bệnh   │
│ nhân.                                                        │
│ Công ty thành viên: [x] Vinmec                                │
│                                                               │
│ Ai đang đau (Actor)? Điều dưỡng tiếp nhận                     │
│                                                               │
│ Workflow thủ công hiện tại (3 bước):                          │
│   1. Bệnh nhân khai triệu chứng ──> 2. Điều dưỡng ước lượng   │
│   mức ưu tiên ──> 3. Xếp hàng chờ khám theo kinh nghiệm       │
│                                                               │
│ Bước nào tốn thời gian/lỗi nhất? Bước 2 (chủ quan, dễ sai)    │
│ AI có thể nhảy vào hỗ trợ ở bước nào? Bước 2 (gợi ý mức ưu    │
│ tiên dạng draft dựa trên triệu chứng nhập)                    │
│                                                               │
│ Đo thành công bằng gì (Metric có số)?                         │
│   "Giảm thời gian chờ trung bình của ca khẩn cấp thực sự"     │
│                                                               │
│ Quick Architecture: [ ] No AI  [x] LLM  [ ] Agent (bắt buộc   │
│ HITL — bác sĩ/điều dưỡng luôn quyết định cuối cùng)           │
└─────────────────────────────────────────────────────────────┘
```

---

# 🗳️ Quyết định lựa chọn của nhóm

Nhóm chọn **Card #1 — VinFast: Ưu tiên hoá cảnh báo bảo trì pin** để thực hiện Deep-Dive.

**Lý do lựa chọn:**
- Metric có số rõ ràng, dễ đo (thời gian rà soát cảnh báo, tỉ lệ bỏ sót cảnh báo nghiêm trọng).
- Ranh giới an toàn (Operational Boundary) dễ định nghĩa và test adversarial, phù hợp với Phase 4.
- Không cần kiến trúc Multi-Agent phức tạp — một LLM Feature kết hợp Rule cứng cho ngưỡng an toàn là đủ, đúng tinh thần "Problem First, AI Second".

**Lý do loại các thẻ khác:**
- **Card #2 (Xanh SM điểm đón):** Bài toán tốt nhưng ít rủi ro vận hành hơn, phù hợp làm phương án dự phòng nếu Card #1 gặp khó khăn dữ liệu.
- **Card #3 (Vinmec triage):** Rủi ro cao nhất (y tế), cần Operational Boundary cực kỳ nghiêm ngặt và nhiều vòng duyệt hơn — vượt phạm vi 85 phút Deep-Dive của buổi lab.
