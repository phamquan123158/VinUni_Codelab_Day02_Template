# Problem Scan — Các cơ hội AI trong hệ sinh thái Vingroup

Bài làm phát triển từ bốn ý tưởng người học đã cung cấp: đặt lịch Vinmec, đặt đồ ăn Vinhomes, theo dõi bệnh nhân Vinmec và gợi ý đặt xe/voucher kèm cảnh báo pin Xanh SM. Tách cảnh báo pin thành bài toán thứ năm vì có actor, dữ liệu và giới hạn riêng.

> Đây là các đề xuất học tập, chưa có khảo sát xác minh quy trình doanh nghiệp. Thời gian và metric trong các thẻ là giả định/mục tiêu thử nghiệm, không phải kết quả đã đo.

## Phase 1 — SCAN

| # | Đơn vị | Lens | Vấn đề cần giải quyết |
|---|---|---|---|
| 1 | Vinmec | Tốn thời gian | Người bệnh khó tìm lịch bác sĩ phù hợp với mô tả nhu cầu; nhân viên phải hỏi lại, đối chiếu chuyên khoa và lịch trống nhiều lần. |
| 2 | Vinhomes | AI có thể tốt hơn | Cư dân phải tự tìm đồ ăn, đối chiếu voucher, chọn món bổ sung và kiểm tra giao hàng đến căn hộ qua nhiều bước. |
| 3 | Vinmec | Pain từ người khác | Nhân viên y tế phải theo dõi thông tin bệnh nhân trong và sau khám; thông tin phân tán có thể làm chậm việc nhận biết trường hợp cần kiểm tra. Đề xuất hỗ trợ tổng hợp và chuyển cảnh báo theo tiêu chí chuyên môn được duyệt. |
| 4 | Xanh SM | Tốn thời gian | Khách phải đối chiếu loại xe/tài xế khả dụng và voucher để tìm phương án phù hợp số người, hành lý, ngân sách. Phạm vi đầu tiên là gợi ý loại xe; việc ghép tài xế theo hệ thống điều phối. |
| 5 | Xanh SM | Lặp lại | Tài xế phải theo dõi pin và đối chiếu nhu cầu hành trình; đề xuất hỗ trợ cảnh báo cần kiểm tra pin trước chuyến. Tách từ ý tưởng #4, cần dữ liệu xe và quy tắc vận hành được phê duyệt. |

## Phase 2 — QUICK-ASSESS

Chọn #1, #2 và #4 để lập ba thẻ. #3 và #5 cần dữ liệu theo thời gian cùng tiêu chí an toàn đã được người phụ trách xác nhận trước khi thử nghiệm.
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
| **Metric có số** | Giảm thời gian trung bình từ nhập nhu cầu đến kiểm tra trạng thái ghép chuyến từ **8 xuống ≤3 phút thao tác/lượt**; ít nhất **95%** đề xuất đáp ứng tiêu chí đã khai báo trên **100 ca mẫu**; **100%** voucher đề xuất hợp lệ với điều kiện của dữ liệu test. Thời gian này không bao gồm chờ tài xế đến. |
| **Quick Architecture** | **[x] Rule + [x] LLM; [ ] Agent; [ ] No AI.** LLM trích xuất nhu cầu; rule lọc loại xe, kiểm tra voucher và dùng dịch vụ điều phối hiện có. |
| **Giới hạn và fallback** | Không bịa tài xế, giá, ETA hoặc mã ưu đãi; không cam kết chắc chắn có xe. Chỉ gửi yêu cầu đặt chuyến sau khi khách xác nhận. Nếu thiếu báo giá/khả dụng, yêu cầu tải lại hoặc dùng luồng đặt xe hiện có. |

**Workflow hiện tại giả định — 5 bước:**

1. Khách nhập điểm đón, điểm đến và nhu cầu chuyến đi (**1 phút**).
2. So sánh loại xe, số chỗ, khả năng chở hành lý và báo giá (**3 phút**).
3. Tìm và thử các voucher cho chuyến đi (**2 phút**).
4. Kiểm tra tổng tiền và xác nhận yêu cầu đặt xe (**1 phút**).
5. Hệ thống tìm tài xế; khách kiểm tra trạng thái ghép chuyến, xử lý lựa chọn khác nếu chưa có xe (**1 phút thao tác giả định**).

**Tổng: 8 phút thao tác/lượt.** Ý tưởng cảnh báo pin cho tài xế được tách thành bài toán riêng vì cần dữ liệu xe, lộ trình và quy trình vận hành; không gộp vào prototype gợi ý chuyến/voucher. Cần báo giá, thông tin loại xe, dữ liệu khả dụng và điều kiện voucher từ hệ thống. Nếu người dùng chọn đủ tiêu chí trên giao diện, rule và bộ lọc có thể xử lý mà không cần LLM.

## Lựa chọn cho Deep-Dive

Chọn **Card #2 — Gợi ý giỏ đồ ăn và voucher hợp lệ cho cư dân Vinhomes**. Bài toán có đầu vào dễ mô phỏng (thực đơn, ngân sách, điều kiện voucher), đầu ra có thể đối chiếu bằng code và điểm xác nhận rõ ràng ở người mua. Phạm vi ban đầu là một khu đô thị, mỗi giỏ thuộc một cửa hàng.

Vinmec đặt lịch cần danh mục và quy trình chuyển nhân viên chuyên môn; Xanh SM cần báo giá và dữ liệu điều phối. Chưa có các nguồn dữ liệu này để chứng minh hiệu quả. Lựa chọn Vinhomes là quyết định scoping cho bài lab, chưa phải kết luận về giá trị kinh doanh lớn nhất.