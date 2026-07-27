# 01 — Individual Problem Scan

## Scan rộng

| # | Lăng kính | Problem quan sát được | Ai chịu ảnh hưởng? | Dấu hiệu thật |
|---|---|---|---|---|
| 1 | Tốn thời gian | Không biết nấu gì cho phù hợp | Bất cứ ai có nhu cầu nấu ăn | Mất 30-60 phút cho chọn đồ ăn, xảy ra nhiều lần, nhiều người gặp |
| 2 | Lặp lại + Tốn thời gian | Thống kê thu chi của cửa hàng | Chủ tiệm | Hàng ngày |
| 3 | Tốn thời gian + AI có thể làm tốt hơn | Khó khăn lập kế hoạch | Sinh viên | Mất thời gian dài để đáp ứng hết yêu cầu theo ngữ cảnh, khó phân loại các công việc/môn học |
| 4 | Tốn thời gian + Lặp lại | Chỉnh sửa đơn xin việc theo từng công ty | Người xin việc | Mất thời gian tìm hiểu, review, chỉnh sửa và đánh giá phù hợp với công ty |
| 5 | Tốn thời gian + AI có thể làm tốt hơn | Lập lịch du lịch | Người đi du lịch | Mất thời gian tìm hiểu, review, so sánh giữa các địa điểm, chi phí |

Vì sao phần scan này mạnh:

- Có 4 lăng kính khác nhau được dùng (Tốn thời gian, Lặp lại, AI có thể làm tốt hơn), không chỉ dựa vào một góc nhìn.
- Mỗi problem có actor cụ thể và dấu hiệu thật kèm ước lượng thời gian.
- Không có ý nào bắt đầu bằng "làm chatbot" hoặc "xây agent" — tất cả xuất phát từ pain quan sát được.

Điểm cần lưu ý để cải thiện nếu làm lại:

- Problem #3 (khó khăn lập kế hoạch) và #5 (lập lịch du lịch) khá gần nhau về bản chất (đều là "tổng hợp thông tin + sắp xếp theo ràng buộc"), nên khi hội tụ nhóm có thể bị coi là cùng một cluster.
- Dấu hiệu thật ở #3 và #4 chưa có con số cụ thể (chưa ghi rõ bao nhiêu phút/lần) — nên bổ sung số liệu ước lượng trước khi pitch.

## Top 3

| Rank | Problem | Vì sao chọn | Điều còn chưa chắc |
|---|---|---|---|
| 1 | Thống kê thu chi cho cửa hàng | Actor rõ, AI có thể giúp thống kê | Những thông tin bảo mật riêng của cửa hàng, quyền bảo vệ riêng tư |
| 2 | Không biết nấu gì cho phù hợp | Actor phổ biến, tần suất cao (gần như hàng ngày), dễ đo bằng phút/lần | Dữ liệu lớn, cần nhiều dữ liệu để áp dụng được hết trường hợp |
| 3 | Lập lịch du lịch | Actor rõ, impact lớn | Workflow phức tạp |

---

## Problem Card #1 — Không biết nấu gì cho phù hợp


**Problem 1 câu:** 
Mỗi lần chuẩn bị bữa ăn, người nấu mất 30-60 phút để quyết định nấu món gì phù hợp với nguyên liệu và khẩu vị.

**Actor:**
Bất kỳ ai tự nấu ăn thường xuyên (dân văn phòng, sinh viên ở trọ, người nội trợ).

**Thời điểm / bối cảnh:**
Trước mỗi bữa ăn, đặc biệt là sau giờ làm/học khi còn ít thời gian và năng lượng để suy nghĩ.

**Current workflow 3-7 bước:**
```text
1. Mở tủ lạnh/tủ bếp xem còn nguyên liệu gì
2. Tìm kiếm công thức trên Google/Cookpad/hội nhóm Facebook
3. So sánh nhiều công thức (độ khó, thời gian nấu, khẩu vị)
4. Chốt món, kiểm tra còn thiếu nguyên liệu gì không
5. Đi chợ/mua thêm nếu cần rồi nấu
```

**Bottleneck:**
Bước 2-3 — tìm kiếm và so sánh công thức mất 20-40 phút vì quá nhiều lựa chọn và khó biết công thức nào hợp khẩu vị/thời gian hiện có.

**Impact:**
30-60 phút/lần, xảy ra gần như mỗi ngày. Mỗi lần tiết kiệm không lớn tuyệt đối, nhưng cộng dồn theo thời gian và theo số lượng người gặp là rất lớn.

**Success metric:**
Giảm thời gian chọn món từ khoảng 45 phút xuống dưới 10 phút/lần.

**Non-AI alternative:**
Lên thực đơn tuần cố định trước (meal plan). Giảm việc phải quyết định mỗi ngày, nhưng kém linh hoạt khi nguyên liệu thực tế trong tủ lạnh thay đổi.

**AI hypothesis:**
AI gợi ý 3-5 món dựa trên nguyên liệu hiện có, khẩu vị và thời gian nấu; người dùng chỉ cần chọn 1 trong các gợi ý thay vì tự tìm và so sánh.

**Quick gut:**
[x] Rule / Workflow (bài toán khá đơn giản — tra công thức theo nguyên liệu — chưa chắc cần Agent)

### Draft current workflow

```text
CURRENT STATE — ~45 phút/lần

[1 Xem nguyên liệu có sẵn: 5']
→ [2 Tìm công thức online: 20']   <-- bottleneck
→ [3 So sánh công thức: 30']      <-- bottleneck
→ [4 Chốt món + check thiếu gì: 5']
→ [5 Mua thêm nếu cần + nấu]
```

### Draft future workflow

```text
FUTURE STATE — ~8 phút/lần

[1 Nhập/chụp ảnh nguyên liệu có sẵn: 2']
→ [2 AI gợi ý 3-5 món phù hợp: tự động]
→ [3 Người dùng chọn 1 món: 3']   <-- human boundary
→ [4 Nhận công thức + list cần mua thêm: 3']

Fallback: Không món nào hợp → người dùng tự tìm như cũ.
```

---

## Problem Card #2 — Thống kê thu chi cửa hàng

**Problem 1 câu:**  
Mỗi ngày chủ tiệm mất khoảng 30-60 phút để ghi chép, cộng tổng và đối soát thu chi thủ công, dễ sai sót.

**Actor:**
Chủ tiệm nhỏ (quán ăn, tạp hóa, quán cà phê) tự quản lý sổ sách, không có kế toán riêng.

**Thời điểm / bối cảnh:**
Cuối mỗi ngày bán hàng, trước khi đóng cửa hoặc trước khi ngủ.

**Current workflow:**
```text
1. Ghi hóa đơn/thu chi vào sổ tay hoặc Excel rải rác trong ngày
2. Cuối ngày cộng tổng doanh thu và chi phí
3. Đối chiếu số liệu với tiền mặt thực tế trong két
4. Ghi chú các khoản bất thường (nếu có, tìm lại nguyên nhân lệch)
5. Tổng hợp thành báo cáo tuần/tháng khi cần
```

**Bottleneck:** 
Bước 2-3 — cộng tổng và đối soát mất 30-45 phút vì dữ liệu được ghi rải rác cả ngày, dễ nhầm hoặc bỏ sót khoản nhỏ.

**Impact:**
30-60 phút/ngày x 7 ngày/tuần cho 1 chủ tiệm. Sai sót đối soát ảnh hưởng trực tiếp đến tiền bạc thật, không chỉ là mất thời gian.

**Success metric:**
Giảm thời gian đối soát cuối ngày từ khoảng 45 phút xuống dưới 15 phút; giảm số lần lệch sổ sách xuống gần 0/tháng.

**Non-AI alternative:**
Máy POS có sẵn tổng hợp doanh thu tự động, hoặc template Excel có công thức tính sẵn. Giải quyết được phần cộng tổng, nhưng chưa xử lý tốt phần phân loại khoản chi lặt vặt và giải thích khoản bất thường.

**AI hypothesis:**
AI hỗ trợ nhập nhanh (chụp ảnh hóa đơn hoặc gõ tin nhắn ngắn), tự phân loại thu/chi, tổng hợp báo cáo ngày/tuần và cảnh báo khi số liệu bất thường. Chủ tiệm vẫn là người xác nhận số liệu cuối cùng.

**Quick gut:**
[x] Workflow

### Draft current workflow

```text
CURRENT STATE — ~50 phút/ngày

[1 Ghi chép rải rác trong ngày: ~15']
→ [2 Cộng tổng cuối ngày: 20']   <-- bottleneck
→ [3 Đối soát tiền mặt: 15']     <-- bottleneck
→ [4 Ghi chú bất thường: 5']
→ [5 Tổng hợp báo cáo tuần/tháng: khi cần]
```

### Draft future workflow

```text
FUTURE STATE — ~15 phút/ngày

[1 Chụp ảnh hóa đơn / nhắn nhanh: 5']
→ [2 AI phân loại thu/chi: tự động]
→ [3 AI tổng hợp + cảnh báo bất thường: tự động]
→ [4 Chủ tiệm xác nhận số liệu: 10']   <-- human boundary

Fallback: AI phân loại sai → chủ tiệm tự sửa tay trong bước xác nhận.
```

---


## Problem Card #3 — Lập lịch du lịch

**Problem 1 câu:**
Người đi du lịch mất nhiều giờ để tìm hiểu, so sánh địa điểm và chi phí trước khi chốt được lịch trình.

**Actor:**
Người hoặc nhóm tự lên kế hoạch du lịch, không dùng tour trọn gói.

**Thời điểm / bối cảnh:**
Vài tuần trước chuyến đi, khi bắt đầu lên kế hoạch chi tiết.

**Current workflow 3-7 bước:**
```text
1. Xác định điểm đến và số ngày đi
2. Tìm hiểu địa điểm tham quan, đọc review trên nhiều nền tảng (blog, TripAdvisor, Google Maps)
3. So sánh chi phí: vé, khách sạn, ăn uống, di chuyển
4. Sắp xếp lịch trình theo ngày, tính khoảng cách/thời gian di chuyển
5. Đặt chỗ (vé, khách sạn)
```

**Bottleneck:**
Bước 2-3 — tìm hiểu và so sánh trên nhiều nguồn rời rạc mất 2-5 giờ vì phải tự tổng hợp thông tin phân tán.

**Impact:**
2-5 giờ/chuyến. Tần suất thấp hơn 2 problem trên (không xảy ra hàng ngày), nhưng mỗi lần dồn vào một khối thời gian lớn và dễ đo.

**Success metric:**
Giảm tổng thời gian nghiên cứu từ khoảng 4 giờ xuống dưới 1 giờ/chuyến.

**Non-AI alternative:**
Dùng tour trọn gói có sẵn. Giảm effort gần như hoàn toàn, nhưng mất tính cá nhân hóa theo sở thích, ngân sách và thời gian rảnh của từng người.

**AI hypothesis:**
AI tổng hợp và đề xuất lịch trình theo ngày kèm chi phí ước tính, dựa trên điểm đến, ngân sách, số ngày và sở thích; người dùng chỉnh sửa nhẹ rồi chốt.

**Quick gut:**
[x] Chưa biết — nghiêng về Agent vì cần tổng hợp nhiều nguồn dữ liệu (giá vé, khách sạn, review) và có thể cần điều chỉnh linh hoạt theo phản hồi, nhưng có thể hạ về Workflow nếu chỉ cần gợi ý tĩnh một lần

### Draft current workflow

```text
CURRENT STATE — ~4 giờ/chuyến

[1 Xác định điểm đến/số ngày: 15']
→ [2 Tìm hiểu & đọc review: 90']   <-- bottleneck
→ [3 So sánh chi phí: 60']         <-- bottleneck
→ [4 Sắp lịch trình: 45']
→ [5 Đặt chỗ: 30']
```

### Draft future workflow

```text
FUTURE STATE — ~1 giờ/chuyến

[1 Nhập điểm đến, ngày, ngân sách, sở thích: 5']
→ [2 AI tổng hợp & đề xuất lịch trình + chi phí ước tính: tự động]
→ [3 Người dùng chỉnh sửa nhẹ: 30']   <-- human boundary
→ [4 Đặt chỗ: 20']

Fallback: Gợi ý không hợp ngân sách/sở thích → người dùng tự tìm hiểu lại như cũ.
```