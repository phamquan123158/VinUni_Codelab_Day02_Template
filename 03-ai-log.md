# AI Log & Reflection — Phiên làm bài AI Product Scoping

> Nhật ký ghi nhận trao đổi thực tế trong phiên hỗ trợ. Chưa có phỏng vấn doanh nghiệp hoặc kiểm thử prototype Vinhomes. Thông tin cá nhân và nhận xét riêng của người học cần được bổ sung trước khi nộp.

## 1. Ý tưởng đầu vào và vai trò của AI

Người học đưa ra bốn ý tưởng: gợi ý đặt lịch Vinmec, gợi ý đồ ăn/voucher cho cư dân Vinhomes, theo dõi tình trạng bệnh nhân và gợi ý đặt xe/voucher kèm cảnh báo pin Xanh SM. AI hỗ trợ chuyển các mô tả sản phẩm thành bài toán có actor, quy trình, điểm nghẽn và metric.

| Yêu cầu đã trao đổi | AI hỗ trợ | Kết quả / kiểm chứng |
|---|---|---|
| Tóm tắt worksheet và các tài liệu | Tổng hợp yêu cầu, cách chấm và quy định nộp bài. | Đã đọc tài liệu trong repository; phát hiện số lens/test không thống nhất giữa các phần. |
| Hoàn thiện TODO Python | Viết system prompt, hàm gọi Gemini và 3 test đối kháng cho bài mẫu pin Xanh SM. | Đã đạt 3 kiểm tra tĩnh và kiểm thử mock trước đó; môi trường lúc kiểm tra thiếu API key nên chưa xác nhận chạy Gemini thật. |
| Hoàn thành Phase 2 từ ý tưởng người học | Viết 3 Quick Cards về đặt lịch, giỏ đồ ăn và đặt xe. | Đã ghi vào worksheet; thời gian được gắn nhãn giả định. |
| Tạo 4 file bài nộp dựa trên Phase 1 | Chuẩn hóa 5 vấn đề, chọn giỏ đồ ăn Vinhomes để deep-dive, vẽ sơ đồ hiện tại. | Ý tưởng thứ 5 là phần cảnh báo pin tách từ ý tưởng Xanh SM của người học. Lựa chọn deep-dive do AI đề xuất theo phạm vi lab, chưa phải quyết định qua họp nhóm. |

## 2. Các điều chỉnh quan trọng

- **Tách bài toán quá rộng:** Đặt xe/voucher và cảnh báo pin có actor, dữ liệu và ràng buộc khác nhau. Tách chúng giúp xác định metric riêng.
- **Giới hạn mua sắm:** Thu hẹp từ mua nhiều loại vật phẩm xuống giỏ đồ ăn của một cửa hàng trong một khu đô thị. Món bổ sung là đề xuất, cần người mua đồng ý.
- **Chia trách nhiệm công nghệ:** LLM hiểu câu nhập tự do; code kiểm tra voucher và tính tiền. Không dùng LLM làm nguồn giá hoặc tự quyết định thanh toán.
- **Phân biệt giả định với bằng chứng:** Các con số 16 phút, mục tiêu 5 phút, 100 giỏ test và 20 lượt thử chưa phải quan sát thực tế. Không suy diễn thành doanh thu tăng.

## 3. Điểm AI chưa làm đủ và cách xử lý

Bảng Phase 1 trên file đã lưu còn trống, trong khi các ý tưởng nằm trong hội thoại. AI dùng lại đúng bốn ý tưởng đã cung cấp, ghi rõ phần tách thành ý tưởng thứ năm để người học rà soát.

Quick Card Xanh SM trước đó ghi thời gian 8 phút đến xác nhận nhưng cộng cả bước kiểm tra ghép chuyến sau xác nhận. Trong file scan mới, mốc đo được sửa thành đến kiểm tra trạng thái ghép chuyến để khớp tổng thời gian.

Code Xanh SM trước đây chỉ là bài tập riêng, chưa khớp deep-dive Vinhomes hiện tại. Báo cáo đã nêu rõ chênh lệch và liệt kê test cần triển khai, không trình bày kết quả mock hoặc kiểm tra tĩnh như bằng chứng thành công của sản phẩm Vinhomes.

Kiểm tra JSON, ID và số tiền là cần thiết nhưng chưa đánh giá hết độ phù hợp món ăn hoặc chất lượng giải thích. Cần người dùng thử nghiệm, đối chiếu dữ liệu gốc và so với baseline rule.

## 4. Kết quả hiện có và còn thiếu

**Đã có:** danh sách vấn đề, 3 Quick Cards, phân tích 6 trường, thiết kế rule/LLM, sơ đồ quy trình, ranh giới và kế hoạch test.

**Chưa có:** dữ liệu cửa hàng thật, baseline đo được, prototype giỏ đồ ăn, phản hồi Gemini cho bài toán này, khảo sát người dùng, chi phí hoặc ROI. Vì vậy quyết định báo cáo là NOT YET.

## 5. Reflection để người học hoàn thiện

Bài học được rút ra từ quá trình scoping là phải mô tả vấn đề trước khi chọn công nghệ, định nghĩa mốc đo nhất quán và kiểm chứng đề xuất của AI bằng dữ liệu. Quy tắc voucher có thể giải quyết bằng code; LLM chỉ có giá trị nếu giúp người dùng diễn đạt và chọn giỏ hiệu quả hơn.

- Họ tên / mã sinh viên: **Người học bổ sung**.
- Đề xuất của AI mà bản thân đồng ý hoặc không đồng ý, cùng lý do: **Người học bổ sung**.
- Thay đổi do bản thân thực hiện sau khi đọc báo cáo: **Người học bổ sung**.
- Kết quả thử nghiệm thực tế và một ví dụ AI trả lời sai: **Chưa có; bổ sung sau khi triển khai và chạy đúng prototype**.
