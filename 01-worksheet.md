# Lab 02 — Worksheet: AI Product Scoping (Vin Smart Future)

---

## 🏛️ 1. Bối cảnh thực tế: Vin Smart Future (Vingroup)

**Vingroup** — Tập đoàn tư nhân lớn nhất Việt Nam — vừa sáp nhập toàn bộ các phòng ban công nghệ thuộc các công ty thành viên thành một đơn vị công nghệ thống nhất mang tên **Vin Smart Future**. 

Nhiệm vụ của **Vin Smart Future** là xây dựng các giải pháp AI, số hóa, và tự động hóa cốt lõi để nâng cao hiệu suất vận hành và trải nghiệm khách hàng xuyên suốt các công ty thành viên:
* 🚗 **VinFast:** Hệ thống xe điện thông minh (EV), trợ lý AI ảo trong xe, dự đoán bảo trì pin, và quản lý chuỗi cung ứng sản xuất.
* 🚕 **Xanh SM (GSM):** Vận hành đội xe taxi/xe máy điện thông minh, điều vận thông minh (Smart Dispatching), tối ưu hóa lộ trình di chuyển.
* 🏢 **Vinhomes:** Quản lý đô thị thông minh (Smart Cities), trợ lý cư dân thông minh, tối ưu hóa mức tiêu thụ năng lượng.
* 🏥 **Vinmec:** Y tế thông minh, chẩn đoán hình ảnh bằng AI, tối ưu hóa quản lý hồ sơ bệnh án.
* 🎢 **Vinpearl / VinWonders:** Trải nghiệm du lịch số hóa, quản lý phòng và luồng khách thông minh tại các khu vui chơi.

Trong buổi Lab hôm nay, nhóm của bạn sẽ đóng vai trò là **AI Product Engineer** tại **Vin Smart Future**, tiến hành tìm kiếm, scoping, phân tích độ khả thi, thiết lập ranh giới vận hành, và xây dựng một **bản mẫu kỹ thuật (prompt prototype)** cho một bài toán cụ thể thuộc một trong những mảng kinh doanh trên.

---

## 📊 2. Cơ cấu tính điểm bài lab

### 👥 Điểm nhóm (60 điểm)

| Gate | Điểm | Deliverable | Tiêu chí chấm |
|---|---:|---|---|
| **G1. Workflow Mapping** | 20 | Problem Deep-Dive | Vẽ chi tiết quy trình hiện tại: các bước, handoff, thời gian, bottleneck |
| **G2. Problem Statement** | 20 | Problem Deep-Dive | Problem Statement 6-field bám sát thực tế, metric có số và ranh giới rõ ràng |
| **G3. AI Fit & Future Flow** | 10 | Problem Deep-Dive | So sánh Rule vs LLM vs Agent, future flow có bước AI, ranh giới và Fallback |
| **G4. Decision Quality** | 10 | Problem Deep-Dive | Quyết định Go/Not Yet/No-Go trung thực và có chứng cứ rõ ràng |

### 👤 Điểm cá nhân (40 điểm)

| Gate | Điểm | Deliverable | Tiêu chí chấm |
|---|---:|---|---|
| **I1. Scan & Cards** | 15 | Quick Cards | Liệt kê 5 problems sử dụng 3 lenses, hoàn thiện 3 quick cards chất lượng |
| **I2. Prototyping** | 10 | 02-lab/ | Chạy thử nghiệm programmatic prompt prototype thành công |
| **I3. AI Log & Reflection** | 15 | 03-ai-log.md | Phản ánh trung thực về việc dùng AI làm thought-partner (giúp gì, sai gì, sửa gì) |

---

# 🚀 Phase 0 — worked Example: Xanh SM Intelligent Dispatcher (15 min)

*Giảng viên walk-through ví dụ thực tế từ Vin Smart Future để bạn hiểu rõ cách scoping một bài toán AI.*
Đọc chi tiết worked example tại file [02-deliverable-example.md](02-deliverable-example.md).

---

# 🔍 Phase 1 — SCAN (Cá nhân, 20 min)

Hãy sử dụng **4 Lenses** dưới đây để quét qua hoạt động vận hành của các công ty thành viên Vingroup. Ghi lại **ít nhất 5 bài toán/bottleneck** thực tế.

### 4 Lenses tìm bài toán AI cho Vingroup:
1. **Lặp lại (Repetitive):** Tác vụ lặp đi lặp lại nhiều lần hằng ngày. (Ví dụ: So khớp hóa đơn sạc điện tại VinFast, route lại chuyến taxi tại Xanh SM).
2. **Tốn thời gian (Time-consuming):** Tác vụ ngốn thời gian xử lý thủ công của nhân viên. (Ví dụ: Soạn thảo phản hồi đánh giá 1-star của cư dân Vinhomes).
3. **AI có thể tốt hơn (AI-upgrade):** Dịch vụ khách hàng hiện tại còn chậm hoặc phản hồi rập khuôn. (Ví dụ: Chatbot CSKH Vinpearl hỗ trợ đặt vé vui chơi).
4. **Pain từ người khác (Stakeholder Pain):** Bottleneck khiến khách hàng hoặc nhân viên thực địa phàn nàn. (Ví dụ: Tài xế Xanh SM phàn nàn về việc hệ thống gợi ý điểm đón khách không chính xác).

> [!TIP]
> **🤖 AI Prompts — Partner brainstorm:**
> Hãy sử dụng prompt sau để brainstorm các bài toán thực tế nếu bạn chưa có ý tưởng:
> *"Tôi là AI Engineer tại Vin Smart Future (Vingroup). Tôi đang tìm kiếm các pain point vận hành cụ thể có thể tối ưu bằng AI cho mảng [Chọn một: VinFast / Xanh SM / Vinhomes / Vinmec]. Hãy gợi ý cho tôi 5 quy trình nghiệp vụ thủ công, tốn nhiều thời gian và gây rò rỉ hiệu suất kèm con số thống kê ước tính về tổn thất."*

### 📝 List bài toán của tôi:
| # | Subsidiary (VinFast/Xanh SM...) | Lens | Mô tả ngắn bài toán |
|---|----------------------------------|------|---------------------|
| 1 | | | |
| 2 | | | |
| 3 | | | |
| 4 | | | |
| 5 | | | |

---

# 🃏 Phase 2 — QUICK-ASSESS (Cá nhân, 30 min)

Chọn **top 3 bài toán** từ danh sách trên và hoàn thiện **3 Quick Problem Cards** dưới đây (10 phút/card).

**Lựa chọn:** Ý tưởng #1 (đặt lịch Vinmec), #2 (đặt đồ ăn Vinhomes) và #4 (đặt xe Xanh SM) từ danh sách đã đề xuất. Ý tưởng #3 về theo dõi bệnh nhân chưa ưu tiên ở bước này vì cần dữ liệu theo thời gian và tiêu chí cảnh báo do nhân viên y tế xác lập.

> Các quy trình, thời gian hiện tại và ngưỡng thành công dưới đây là **giả định phục vụ bài lab**, chưa phải kết quả khảo sát hoặc thử nghiệm. Cần xác minh với người dùng trước khi triển khai. “RC” được hiểu là gợi ý/đề xuất phù hợp với nhu cầu.

### Quick Problem Card #1 — Vinmec: Hỗ trợ tìm lịch khám phù hợp

| Trường | Nội dung |
|---|---|
| **Bài toán (1 câu)** | Người bệnh mất thời gian mô tả nhu cầu, tìm chuyên khoa và đối chiếu lịch bác sĩ để chọn được lịch khám phù hợp. |
| **Công ty thành viên** | Vinmec. |
| **Ai đang đau (Actor)?** | Người bệnh chưa biết bắt đầu đặt lịch ở đâu; nhân viên đặt lịch phải hỏi lại thông tin và tra cứu nhiều lần. |
| **Lens** | Tốn thời gian; pain từ người khác. |
| **Bước tốn thời gian/lỗi nhất** | Bước 2–3: làm rõ nhu cầu và tìm lịch phù hợp, giả định **8 phút/lượt**; có thể phải chuyển lại cho nhân viên chuyên môn khi thông tin không rõ. |
| **AI hỗ trợ ở đâu?** | Bước 2: tóm tắt mô tả của người bệnh thành thông tin có cấu trúc, gợi ý câu hỏi bổ sung và nhóm chuyên khoa dựa trên danh mục được Vinmec phê duyệt. Bước 3: hệ thống lọc lịch có thật theo chuyên khoa, cơ sở và thời gian; AI trình bày các lựa chọn để người bệnh xác nhận. |
| **Metric có số** | Giảm thời gian trung bình từ tiếp nhận đến chọn được lịch từ **15 xuống ≤5 phút/lượt**; trên **100 tình huống mẫu** được nhân viên chuyên môn gán nhãn, ít nhất **95%** được chuyển đúng luồng đặt lịch hoặc luồng cần người hỗ trợ. |
| **Quick Architecture** | **[x] Rule + [x] LLM; [ ] Agent; [ ] No AI.** Rule kiểm tra lịch trống và ràng buộc; LLM xử lý mô tả tự do. Chưa cần Agent tự đặt lịch. |
| **Giới hạn và fallback** | Không chẩn đoán, kê thuốc hoặc tự kết luận mức độ an toàn từ triệu chứng. Ca ngoài phạm vi hoặc thiếu thông tin được chuyển nhân viên chuyên môn theo quy trình đã phê duyệt. Không bịa bác sĩ/lịch trống; chỉ xác nhận đặt lịch khi người bệnh đồng ý và hệ thống đặt lịch báo thành công. |

**Workflow hiện tại giả định — 5 bước:**

1. Người bệnh gọi tổng đài hoặc mở trang đặt lịch, cung cấp nhu cầu (**2 phút**).
2. Nhân viên hỏi thêm và xác nhận thông tin cần cho việc chọn chuyên khoa (**4 phút**).
3. Nhân viên tra cứu bác sĩ, cơ sở và lịch trống phù hợp (**4 phút**).
4. Người bệnh so sánh và chọn khung giờ (**3 phút**).
5. Nhân viên xác nhận, ghi nhận lịch và gửi thông tin hẹn (**2 phút**).

**Tổng: 15 phút/lượt.** Dữ liệu cần có: danh mục chuyên khoa được duyệt, danh sách bác sĩ, lịch trống và quy trình chuyển nhân viên hỗ trợ. Nếu biểu mẫu và bộ lọc thông thường đã đạt mục tiêu, có thể bỏ phần LLM.

### Quick Problem Card #2 — Vinhomes: Gợi ý giỏ đồ ăn và voucher hợp lệ

| Trường | Nội dung |
|---|---|
| **Bài toán (1 câu)** | Cư dân phải tự tìm món và thử nhiều voucher ở các cửa hàng trong khu đô thị để có giỏ đồ ăn phù hợp ngân sách và giao được đến căn hộ. |
| **Công ty thành viên** | Vinhomes — ý tưởng dịch vụ cho cư dân trong khu đô thị. |
| **Ai đang đau (Actor)?** | Cư dân đặt đồ ăn; nhân viên cửa hàng phải giải thích điều kiện ưu đãi và phạm vi giao hàng. |
| **Lens** | Tốn thời gian; AI có thể tốt hơn. |
| **Bước tốn thời gian/lỗi nhất** | Bước 2–3: so sánh món, phí giao và thử voucher, giả định **10 phút/lượt**; dễ chọn mã hết hạn, không đủ giá trị đơn tối thiểu hoặc không áp dụng cho cửa hàng. |
| **AI hỗ trợ ở đâu?** | Bước 1–2: hiểu yêu cầu như ngân sách, số người ăn và sở thích; gợi ý món hoặc món bổ sung từ thực đơn hiện có. Bước 3: code kiểm tra điều kiện voucher, tính tổng tiền sau giảm và phí giao; hệ thống xếp hạng các giỏ hợp lệ để cư dân chọn. |
| **Metric có số** | Giảm thời gian trung bình từ bắt đầu tìm món đến có giỏ được người dùng chấp thuận từ **16 xuống ≤5 phút/lượt**; **100%** voucher được đề xuất hợp lệ trên **100 giỏ kiểm thử** với dữ liệu cố định; ít nhất **80%** giỏ đề xuất được chấp thuận mà không đổi món trong thử nghiệm **20 lượt**. |
| **Quick Architecture** | **[x] Rule + [x] LLM; [ ] Agent; [ ] No AI.** Rule lọc cửa hàng, kiểm tra voucher và tính tiền; LLM hiểu nhu cầu và giải thích đề xuất. |
| **Giới hạn và fallback** | Chỉ dùng thực đơn, giá, tồn kho và voucher từ nguồn dữ liệu được cung cấp; không bịa ưu đãi. Không tự thêm món, thanh toán hoặc gửi địa chỉ căn hộ cho cửa hàng khi chưa được người dùng xác nhận. Thiếu dữ liệu thì hiển thị cần kiểm tra hoặc chuyển về tìm kiếm/lọc thủ công. |

**Workflow hiện tại giả định — 5 bước:**

1. Cư dân xác định món muốn ăn và ngân sách (**2 phút**).
2. Tìm cửa hàng giao được đến căn hộ, so sánh thực đơn và chọn món (**5 phút**).
3. Tìm/thử voucher, đối chiếu điều kiện và tổng tiền gồm phí giao (**5 phút**).
4. Điều chỉnh giỏ hàng, quyết định có thêm món hay không (**2 phút**).
5. Kiểm tra địa chỉ, xem tổng tiền và xác nhận đơn (**2 phút**).

**Tổng: 16 phút/lượt.** Phạm vi bản đầu là **đồ ăn trong một khu đô thị**, chưa mở rộng mọi loại hàng hóa. Cần dữ liệu thực đơn, phạm vi giao hàng, phí giao và điều kiện voucher. So sánh với baseline bộ lọc + thuật toán chọn voucher để xác định LLM có tạo thêm giá trị hay không.

### Quick Problem Card #3 — Xanh SM: Gợi ý phương án đặt xe và voucher

| Trường | Nội dung |
|---|---|
| **Bài toán (1 câu)** | Khách hàng mất thời gian chọn phương án xe phù hợp nhu cầu và thử voucher để biết chi phí chuyến đi trước khi xác nhận. |
| **Công ty thành viên** | Xanh SM. |
| **Ai đang đau (Actor)?** | Khách đặt xe cần lựa chọn phù hợp số người, hành lý và ngân sách; tài xế chịu ảnh hưởng khi nhu cầu khách không khớp loại xe. |
| **Lens** | Tốn thời gian; pain từ người khác. |
| **Bước tốn thời gian/lỗi nhất** | Bước 2–3: đối chiếu loại xe và thử ưu đãi, giả định **5 phút/lượt**; dễ chọn xe không đáp ứng nhu cầu hoặc voucher không áp dụng. |
| **AI hỗ trợ ở đâu?** | Bước 1–2: chuyển mô tả nhu cầu thành các tiêu chí đặt xe và giải thích lựa chọn. Bước 3: rule kiểm tra voucher và tính giá dựa trên báo giá thật. Tài xế được ghép bởi hệ thống điều phối theo khả dụng; prototype không giả định khách được chọn một tài xế cụ thể. |
| **Metric có số** | Giảm thời gian trung bình từ nhập nhu cầu đến xác nhận yêu cầu đặt xe từ **8 xuống ≤3 phút/lượt**; ít nhất **95%** đề xuất đáp ứng tiêu chí đã khai báo trên **100 ca mẫu**; **100%** voucher đề xuất hợp lệ với điều kiện của dữ liệu test. Thời gian này không bao gồm chờ tài xế đến. |
| **Quick Architecture** | **[x] Rule + [x] LLM; [ ] Agent; [ ] No AI.** LLM trích xuất nhu cầu; rule lọc loại xe, kiểm tra voucher và dùng dịch vụ điều phối hiện có. |
| **Giới hạn và fallback** | Không bịa tài xế, giá, ETA hoặc mã ưu đãi; không cam kết chắc chắn có xe. Chỉ gửi yêu cầu đặt chuyến sau khi khách xác nhận. Nếu thiếu báo giá/khả dụng, yêu cầu tải lại hoặc dùng luồng đặt xe hiện có. |

**Workflow hiện tại giả định — 5 bước:**

1. Khách nhập điểm đón, điểm đến và nhu cầu chuyến đi (**1 phút**).
2. So sánh loại xe, số chỗ, khả năng chở hành lý và báo giá (**3 phút**).
3. Tìm và thử các voucher cho chuyến đi (**2 phút**).
4. Kiểm tra tổng tiền và xác nhận yêu cầu đặt xe (**1 phút**).
5. Hệ thống tìm tài xế; khách kiểm tra trạng thái ghép chuyến, xử lý lựa chọn khác nếu chưa có xe (**1 phút thao tác giả định**).

**Tổng: 8 phút thao tác/lượt.** Ý tưởng cảnh báo pin cho tài xế được tách thành bài toán riêng vì cần dữ liệu xe, lộ trình và quy trình vận hành; không gộp vào prototype gợi ý chuyến/voucher. Cần báo giá, thông tin loại xe, dữ liệu khả dụng và điều kiện voucher từ hệ thống. Nếu người dùng chọn đủ tiêu chí trên giao diện, rule và bộ lọc có thể xử lý mà không cần LLM.

> [!TIP]
> **🤖 AI Prompts — Stress-Test thẻ bài toán:**
> Hãy dán nội dung thẻ bài toán của bạn vào LLM để nhận phản biện:
> *"Đây là một thẻ bài toán vận hành tôi đề xuất cho Vin Smart Future: [Dán nội dung]. Hãy đóng vai trò là một CFO và Trưởng phòng Vận hành cực kỳ khắt khe, chỉ ra cho tôi 3 điểm yếu về logic, metric, và giải thích vì sao rule-based code thông thường có thể giải quyết bài toán này tốt hơn là dùng AI."*

---

# 🏗️ Phase 3 — DEEP-DIVE (Nhóm, 85 min)

## 3.1. Current-State Workflow Mapping (25 min)
**Vẽ quy trình hiện tại lên bảng/giấy A3.** Sử dụng các ký hiệu:
* 🔴 **Bottleneck:** Bước gây tắc nghẽn, tốn thời gian, hoặc sai sót nhiều nhất.
* 🔄 **Handoff:** Điểm chuyển giao thông tin giữa người và hệ thống, hoặc giữa các bộ phận.
* Ghi rõ thời gian vận hành trung bình: **Tổng cộng = ____ phút/lượt**.

## 3.2. Problem Statement (6-field) & Metrics (15 min)
Điền đầy đủ 6 trường thông tin của bài toán:

| Field | Nội dung chi tiết |
|---|---|
| **1. Actor / Operator** | Ai đang thực hiện tác vụ hằng ngày? |
| **2. Current Workflow** | Mô tả tóm tắt quy trình thủ công hiện tại và công cụ sử dụng. |
| **3. Bottleneck** | Bước nào chậm, lỗi, hoặc cần xử lý ngôn ngữ tự động nhiều nhất? |
| **4. Business Impact** | Tổn thất thực tế đo bằng thời gian, chi phí, hoặc SLA của Vingroup. |
| **5. Success Metric** | AI giải quyết được thì đạt ngưỡng số mấy? (Ví dụ: *"85% vé được phân loại dưới 10s"*). |
| **6. Operational Boundary** | AI được phép làm gì, TUYỆT ĐỐI không được làm gì, điểm nào cần duyệt? |

## 3.3. Future-State Flow & AI Fit (25 min)
* **Xác định mức AI Fit (AI-Fit Matrix):** Giải pháp thuộc nhóm nào? [ ] Rule / State-Machine [ ] LLM Feature [ ] Agentic Loop.
* **Vẽ Future-State Flow:** Đánh dấu rõ:
  * 🔵 **AI Step:** Tác vụ LLM xử lý.
  * 🟢 **Human Step (HITL):** Bước con người phê duyệt/review (Human-in-the-loop).
  * ↩️ **Fallback:** Kế hoạch dự phòng khi LLM trả về kết quả lỗi hoặc không tự tin.

---

# 💻 Phase 4 — TECHNICAL PROMPT PROTOTYPE (Nhóm, 30 min)

Để đảm bảo kỹ sư của Vin Smart Future luôn giữ vững năng lực lập trình, nhóm của bạn sẽ tiến hành **lập trình bản mẫu prompt** trực tiếp trên **Gemini 2.5 Flash** bằng Python để stress-test hệ thống.

### Hướng dẫn thực hiện:
1. Mở file [starter-code/prompt_prototype.py](starter-code/prompt_prototype.py) bằng VS Code/Cursor.
2. Hoàn thiện các nội dung sau:
   * **System Prompt:** Viết chỉ thị cực kỳ nghiêm ngặt quy định vai trò, nhiệm vụ, định dạng output và **Operational Boundary (Ranh giới cấm)** của mô hình.
   * **Structured Output:** Định nghĩa định dạng JSON output rõ ràng.
   * **Adversarial Test Cases:** Viết ít nhất 3 prompts "tấn công" (Adversarial inputs) cố tình dụ AI vượt ranh giới hoặc đưa ra câu trả lời không được phép để kiểm tra xem ranh giới của bạn có thực sự vững chắc.
3. Chạy file python:
   ```bash
   python3 prompt_prototype.py
   ```
4. Kiểm tra xem các ranh giới an toàn có bị LLM phá vỡ hay không và ghi lại kết quả vào worksheet.

---

# 🏁 Phase 5 — EVALUATE (Nhóm, 20 min)

### AI Readiness Checklist:
1. [ ] Chúng tôi có sẵn dữ liệu mẫu/logs sạch để test?
2. [ ] Rủi ro khi AI sai có nằm trong tầm kiểm soát (qua HITL hoặc Fallback)?
3. [ ] Stakeholders sẵn sàng thay đổi quy trình làm việc cũ?

### Quyết định cuối cùng của Ban Giám Đốc Vin Smart Future:
[ ] **GO (Bắt đầu xây dựng Prototype):** Bắt đầu phát triển với scope hẹp.
[ ] **NOT YET (Cần tích lũy thêm dữ liệu/xác lập baseline):** Trì hoãn để chuẩn bị thêm.
[ ] **NO-GO (Không khả thi / Rule-based tốt hơn):** Hủy bỏ dự án AI này.

**Justification (Lý giải quyết định dựa trên bằng chứng kỹ thuật và chi phí):**
> *Viết lý giải chi tiết tại đây*

---

# 📝 Phase 6 — REFLECTION (Cá nhân)
*Ghi nhận phản ánh của cá nhân bạn về việc phối hợp với AI trong buổi học hôm nay vào file `03-ai-log.md`.*
