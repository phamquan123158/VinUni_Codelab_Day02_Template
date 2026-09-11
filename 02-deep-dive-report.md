# 02 — Deep-Dive Report

> Bài toán: **VinFast — Ưu tiên hoá cảnh báo bảo trì pin (Predictive Maintenance Triage)**

---

# 🏗️ Phase 3 — DEEP-DIVE

## 3.1. Current-State Workflow Mapping

```text
┌──────────────┐     ┌──────────────┐     ┌──────────────┐     ┌──────────────┐
│ Bước 1       │     │ Bước 2       │     │ Bước 3       │     │ Bước 4       │
│ Hệ thống nhận│     │ Kỹ thuật viên│     │ Tra cứu lịch │     │ Xếp lịch     │
│ log cảnh báo │ ──→ │ đọc & phân   │ ──→ │ sử bảo dưỡng │ ──→ │ kiểm tra ưu  │
│ telemetry    │     │ loại thủ công│     │ của xe       │     │ tiên         │
│              │     │              │     │              │     │              │
│ Ai: Hệ thống │     │ Ai: Kỹ thuật │     │ Ai: Kỹ thuật │     │ Ai: Kỹ thuật │
│ telemetry    │     │ viên         │     │ viên         │     │ viên         │
│ ⏱ tự động    │     │ ⏱ 5 phút 🔴  │     │ ⏱ 3 phút 🔴  │     │ ⏱ 2 phút     │
│ In: Dữ liệu  │     │ In: Log thô  │     │ In: VIN xe   │     │ In: Mức độ   │
│ cảm biến pin │     │ Out: Mức độ  │     │ Out: Lịch sử │     │ ưu tiên      │
│ /động cơ     │     │ nghi vấn     │     │ bảo dưỡng    │     │ Out: Lịch hẹn│
└──────────────┘     └──────────────┘     └──────────────┘     └──────────────┘
🔴 = Bottleneck   🔄 Handoff: Bước 1→2 (hệ thống → người), Bước 4 (kỹ thuật viên → trung tâm dịch vụ)
⏱ Tổng thời gian xử lý thủ công: ~10-12 phút/cảnh báo × hàng trăm cảnh báo/ngày.
```

## 3.2. Problem Statement (6-field)

| Field | Nội dung chi tiết |
|---|---|
| **1. Actor / Operator** | Kỹ thuật viên trung tâm dịch vụ VinFast (Service Center Technician). |
| **2. Current Workflow** | Hệ thống telemetry gửi hàng trăm cảnh báo pin/động cơ mỗi ngày (nhiệt độ bất thường, sụt điện áp, lỗi cảm biến). Kỹ thuật viên phải tự đọc từng log, đối chiếu ngưỡng an toàn trong tài liệu kỹ thuật, tra cứu lịch sử bảo dưỡng xe, rồi mới quyết định mức độ ưu tiên kiểm tra/triệu hồi. Hoàn toàn thủ công, mất 10-12 phút/cảnh báo. |
| **3. Bottleneck** | Bước 2-3 (mất 8 phút): Đọc log thô và đối chiếu ngưỡng an toàn kỹ thuật đòi hỏi kinh nghiệm chuyên môn, dễ bỏ sót cảnh báo nghiêm trọng khi khối lượng log lớn vào giờ cao điểm. |
| **4. Business Impact** | Trung bình 300-400 cảnh báo/ngày trên toàn hệ thống trung tâm dịch vụ. Ước tính tốn 40-50 giờ nhân lực/ngày để rà soát thủ công. Bỏ sót cảnh báo nghiêm trọng có thể dẫn đến sự cố an toàn (cháy pin, hỏng động cơ giữa đường) và ảnh hưởng uy tín thương hiệu VinFast. |
| **5. Success Metric** | 1. Giảm thời gian rà soát mỗi cảnh báo từ 8 phút xuống dưới 2 phút (Efficiency).<br>2. Tỉ lệ bỏ sót cảnh báo mức độ nghiêm trọng (Critical) giảm về 0% trong tập test (Safety/Quality). |
| **6. Operational Boundary** | AI được phép đọc log telemetry, tra cứu lịch sử bảo dưỡng, và **soạn thảo (draft)** mức độ ưu tiên kèm giải thích ngắn gọn cho kỹ thuật viên xem xét. **CẤM:** AI không được tự động đóng cảnh báo hoặc tự ý huỷ lịch kiểm tra; mọi cảnh báo được AI gắn nhãn "Critical" bắt buộc phải có kỹ thuật viên xác nhận trong vòng 30 phút (Human-in-the-loop bắt buộc). |

## 3.3. Future-State Flow & AI Fit

- **AI Fit:** **LLM Feature kết hợp Rule cứng** cho ngưỡng an toàn (nhiệt độ pin, điện áp) — không cần Agentic Loop tự trị vì quyết định cuối cùng luôn cần con người xác nhận, và ngưỡng an toàn kỹ thuật là cố định, không nên để LLM tự suy luận.

```text
┌──────────────┐     ┌──────────────┐     ┌──────────────┐     ┌──────────────┐
│ Bước 1       │     │ Bước 2       │     │ Bước 3       │     │ Bước 4       │
│ Hệ thống nhận│     │ 🔵 Rule check│     │ 🔵 AI tóm tắt│     │ 🟢 Kỹ thuật  │
│ log cảnh báo │ ──→ │ ngưỡng an    │ ──→ │ log + draft  │ ──→ │ viên duyệt & │
│              │     │ toàn cứng    │     │ mức ưu tiên  │     │ xếp lịch     │
└──────────────┘     └──────────────┘     └──────────────┘     └──────────────┘
                                                                       │
                                                                       ▼
                                                                ↩️ Fallback:
                                                                Nếu AI không tự
                                                                tin phân loại,
                                                                gắn nhãn "Cần
                                                                review thủ công"
                                                                và giữ nguyên
                                                                quy trình cũ.
```

---

# 🏁 Phase 5 — EVALUATE

### AI Readiness Checklist:
1. [x] Chúng tôi có sẵn dữ liệu mẫu/logs sạch để test? (Log telemetry lịch sử có sẵn từ hệ thống VinFast).
2. [x] Rủi ro khi AI sai có nằm trong tầm kiểm soát (qua HITL hoặc Fallback)? (Có — bắt buộc kỹ thuật viên xác nhận, có fallback về quy trình thủ công).
3. [ ] Stakeholders sẵn sàng thay đổi quy trình làm việc cũ? (Cần thêm buổi làm việc với trưởng trung tâm dịch vụ để thống nhất quy trình duyệt mới).

### Quyết định cuối cùng của Ban Giám Đốc Vin Smart Future:

[x] **NOT YET (Cần tích lũy thêm dữ liệu/xác lập baseline):** Trì hoãn để chuẩn bị thêm.

**Justification:**
> Bài toán có metric rõ ràng và Operational Boundary khả thi để kiểm soát rủi ro (Rule cứng cho ngưỡng an toàn + HITL bắt buộc cho cảnh báo Critical), nên về mặt kỹ thuật đủ điều kiện GO. Tuy nhiên, checklist còn thiếu sự đồng thuận từ stakeholders vận hành (trung tâm dịch vụ) về việc thay đổi quy trình xếp lịch hiện tại — đây là điều kiện tiên quyết trước khi triển khai thật để tránh tình trạng AI đề xuất nhưng không ai thực sự dùng. Đề xuất: chạy thử nghiệm nội bộ (shadow mode, AI chỉ gợi ý song song không thay thế) trong 2 tuần để thu thập baseline độ chính xác trước khi quyết định GO chính thức.
