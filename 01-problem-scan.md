# �📄 01-problem-scan.md — Problem Scanning & Quick Assessment

**Dự án:** Quét cơ hội & Đánh giá nhanh bài toán AI (Phase 1 & Phase 2)  
**Đơn vị thực hiện:** Vin Smart Future — Đơn vị Công nghệ Cốt lõi Vingroup  
**Tác giả:** Kỹ sư AI (Branch `tdat`)  

---

# 🔍 Phase 1 — SCAN: Quét Tìm Cơ Hội AI (4 Lenses)

Sử dụng **4 Lenses** (*Lặp lại, Tốn thời gian, AI-upgrade, Pain từ người khác*) để quét qua hoạt động vận hành của các công ty thành viên trong hệ sinh thái Vingroup.

### 📝 Bảng Quét Cơ Hội (SCAN Opportunity Table)

| # | Công ty thành viên (Subsidiary) | Lens áp dụng | Mô tả bài toán vận hành thực tế |
|---|---|---|---|
| **1** | **Xanh SM (GSM)** | **Tốn thời gian** | Điều phối viên xử lý thủ công các cuộc gọi khẩn cấp từ tài xế về sự cố sạc pin hoặc xe cạn pin giữa đường (mất 15 phút/lượt tra cứu trạm sạc & soạn SMS). |
| **2** | **VinFast** | **AI-upgrade** | Chẩn đoán sơ bộ mã lỗi kỹ thuật và khoanh vùng nguyên nhân từ mô tả triệu chứng tiếng Việt tự nhiên của khách hàng tại xưởng dịch vụ 3S. |
| **3** | **VinFast** | **Lặp lại** | Tự động phân tích và đối soát log OCPP của hàng chục nghìn phiên sạc V-GREEN bị gián đoạn hoặc lỗi đối soát dòng tiền với ví/ngân hàng. |
| **4** | **Vinhomes** | **Lặp lại (Repetitive)** | Tự động trích xuất nội dung, phân loại mức độ khẩn cấp và định tuyến (route) phiếu phản ánh của cư dân trên App Vinhomes Resident đến đúng ban quản lý tòa nhà. |
| **5** | **Vinmec** | **Pain từ người khác** | Tự động trích xuất dữ liệu lâm sàng từ EMR để soạn thảo bản thảo Tóm tắt bệnh án xuất viện (Discharge Summary) giúp bác sĩ giảm 70% tải hành chính. |
| **6** | **Xanh SM (GSM)** | **Pain từ người khác** | Tự động phân tích bản ghi âm cuộc gọi hủy chuyến và ghi chú của tài xế để phân loại 10 nguyên nhân hủy cuốc phổ biến nhất gây rò rỉ doanh thu. |

---

# 🃏 Phase 2 — QUICK-ASSESS: 3 Quick Problem Cards

Chọn lọc **top 3 bài toán tiềm năng nhất** từ danh sách quét trên để hoàn thiện 3 thẻ đánh giá nhanh (Quick Problem Cards).

---

## 📌 QUICK PROBLEM CARD #1: Xanh SM — Xử lý sự cố sạc pin & cạn pin thực địa

```text
┌────────────────────────────────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #1                                                                  │
│                                                                                        │
│ Bài toán (1 câu): Tài xế Xanh SM báo cáo sự cố hết pin / lỗi sạc giữa đường cần điều   │
│ phối cứu hộ hoặc trạm sạc VinFast trống gần nhất trong giờ cao điểm.                  │
│ Công ty thành viên: [ ] VinFast   [x] Xanh SM (GSM)   [ ] Vinhomes   [ ] Vinmec        │
│                                                                                        │
│ Ai đang đau (Actor)? Điều phối viên (Dispatcher) quá tải; Tài xế taxi điện sốt ruột   │
│                                                                                        │
│ Workflow thủ công hiện tại (5 bước):                                                   │
│   1. Nhận cuộc gọi sự cố ──> 2. Tra GPS xe ──> 3. Tra trạm sạc ──> 4. Soạn SMS         │
│   ──> 5. Điều xe sạc pin di động nếu pin nguy cấp (< 5%)                               │
│                                                                                        │
│ Bước nào tốn thời gian/lỗi nhất? Bước 3 & Bước 4 (⏱ 10 phút/lượt)                     │
│ AI có thể nhảy vào hỗ trợ ở bước nào? Bước 3-4 (Tự động query trạm sạc & draft tin)   │
│                                                                                        │
│ Đo thành công bằng gì (Metric có số)?                                                  │
│   - Giảm thời gian xử lý sự cố từ 15 phút ──> dưới 3 phút/lượt                         │
│   - Tỷ lệ đề xuất trạm sạc phù hợp đạt >= 98%                                          │
│                                                                                        │
│ Quick Architecture: [ ] No AI   [ ] Rule   [x] LLM Feature   [ ] Agentic Loop          │
└────────────────────────────────────────────────────────────────────────────────────────┘
```

---

## 📌 QUICK PROBLEM CARD #2: VinFast — Chẩn đoán lỗi kỹ thuật xe từ mô tả tiếng Việt

```text
┌────────────────────────────────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #2                                                                  │
│                                                                                        │
│ Bài toán (1 câu): Cố vấn dịch vụ xưởng 3S mất nhiều thời gian tra cứu và chẩn đoán mò  │
│ nguyên nhân hư hỏng xe từ mô tả tiếng Việt cảm tính của khách hàng.                    │
│ Công ty thành viên: [x] VinFast   [ ] Xanh SM (GSM)   [ ] Vinhomes   [ ] Vinmec        │
│                                                                                        │
│ Ai đang đau (Actor)? Cố vấn dịch vụ (Service Advisor) & Kỹ thuật viên chẩn đoán xưởng 3S│
│                                                                                        │
│ Workflow thủ công hiện tại (4 bước):                                                   │
│   1. Tiếp nhận & ghi nhận mô tả ──> 2. Đọc mã DTC ──> 3. Lái thử chẩn đoán mò          │
│   ──> 4. Lập phiếu báo giá & phương án sửa chữa                                        │
│                                                                                        │
│ Bước nào tốn thời gian/lỗi nhất? Bước 3 (⏱ 35 - 50 phút/xe không hiện mã lỗi rõ ràng)  │
│ AI có thể nhảy vào hỗ trợ ở bước nào? Bước 2-3 (Map mô tả tiếng Việt với sổ tay TSB)   │
│                                                                                        │
│ Đo thành công bằng gì (Metric có số)?                                                  │
│   - Giảm thời gian chẩn đoán sơ bộ từ 45 phút ──> dưới 10 phút/xe                      │
│   - Tỷ lệ chẩn đoán đúng ngay lần đầu (First-Time-Fix) tăng từ 85% ──> 95%             │
│                                                                                        │
│ Quick Architecture: [ ] No AI   [ ] Rule   [x] LLM Feature   [ ] Agentic Loop          │
└────────────────────────────────────────────────────────────────────────────────────────┘
```

---

## 📌 QUICK PROBLEM CARD #3: Vinhomes — Phân loại & Điều hướng phản ánh cư dân

```text
┌────────────────────────────────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #3                                                                  │
│                                                                                        │
│ Bài toán (1 câu): Ban quản lý tòa nhà xử lý thủ công hàng trăm phiếu phản ánh cư dân   │
│ trên App Vinhomes Resident mỗi ngày gây chậm trễ SLA và phản hồi rập khuôn.            │
│ Công ty thành viên: [ ] VinFast   [ ] Xanh SM (GSM)   [x] Vinhomes   [ ] Vinmec        │
│                                                                                        │
│ Ai đang đau (Actor)? Nhân viên CSKH Ban quản lý tòa nhà & Cư dân khu đô thị Vinhomes   │
│                                                                                        │
│ Workflow thủ công hiện tại (4 bước):                                                   │
│   1. Nhận ticket trên App ──> 2. Đọc & phân loại tay ──> 3. Chuyển giao bộ phận        │
│   ──> 4. Soạn thảo phản hồi cập nhật cho cư dân                                       │
│                                                                                        │
│ Bước nào tốn thời gian/lỗi nhất? Bước 2 & 4 (⏱ 8 - 12 phút/ticket)                     │
│ AI có thể nhảy vào hỗ trợ ở bước nào? Bước 2 (Phân loại intent) & Bước 4 (Draft mẫu)   │
│                                                                                        │
│ Đo thành công bằng gì (Metric có số)?                                                  │
│   - Giảm thời gian định tuyến ticket từ 4 tiếng ──> dưới 30 giây                       │
│   - Tỷ lệ gán đúng tổ kỹ thuật/vệ sinh đạt >= 95%                                      │
│                                                                                        │
│ Quick Architecture: [ ] No AI   [ ] Rule   [x] LLM Feature   [ ] Agentic Loop          │
└────────────────────────────────────────────────────────────────────────────────────────┘
```

---

## 🗳️ Quyết định Lựa chọn Bài toán cho Deep-Dive & Lý Do Đánh Đổi

Nhóm quyết định chọn **Thẻ #1 (Xanh SM — Xử lý sự cố sạc pin & cạn pin thực địa)** để triển khai chi tiết trong [02-deep-dive-report.md](02-deep-dive-report.md).

### Lý do lựa chọn Thẻ #1:
1. **Tính cấp bách thực địa cao (High Operational Impact):** Sự cố cạn pin ảnh hưởng trực tiếp tới tài xế đang lưu thông trên đường, nguy cơ gây ùn tắc giao thông và thất thu cuốc xe trực tiếp trong giờ cao điểm.
2. **Dữ liệu số hóa sẵn có (Data Readiness):** Hệ thống FMS và V-GREEN đã có sẵn API cung cấp toạ độ GPS, dung lượng pin SoC và trạng thái cổng sạc theo thời gian thực.
3. **Ranh giới an toàn rõ ràng (Strict Boundary & High Feasibility):** Quy trình có chốt chặn bắt buộc `[DRAFT_ONLY]` (Human-in-the-loop) và ngưỡng pin nguy cấp `< 5%` rất thích hợp để lập trình kiểm thử ranh giới bằng LLM prompt.

### Lý do tạm hoãn 2 thẻ còn lại:
* **Thẻ #2 (VinFast Chẩn đoán lỗi xe):** Đòi hỏi tích hợp sâu với cơ sở dữ liệu kỹ thuật bảo mật TSB nội bộ của xưởng và cần thiết bị phần cứng OBD vật lý để kiểm chứng thực tế, chưa phù hợp với phạm vi 1 buổi lab scoping.
* **Thẻ #3 (Vinhomes Định tuyến phản ánh):** Phần lớn các phản ánh cư dân có thể giải quyết hiệu quả bằng hệ thống luật (Rule-based Regex / Keyword routing) kết hợp danh mục có sẵn trên App, chưa thực sự cần đến sức mạnh ngôn ngữ của LLM ở giai đoạn này.