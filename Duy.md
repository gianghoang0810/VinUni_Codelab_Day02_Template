# 🚀 AI Product Scoping — Phase 1 & 2 Deliverables
> **Học viên:** Duy • **Tổ chức:** Vin Smart Future (Vingroup)  
> **Nhiệm vụ:** Quét tìm cơ hội AI (Scan) & Đánh giá nhanh bài toán (Quick-Assess)

---

## 🔍 Phase 1 — SCAN: Danh Sách Cơ Hội Ứng Dụng AI (5 Bài Toán)

Sử dụng **4 Lenses** (*Lặp lại*, *Tốn thời gian*, *AI nâng cấp*, *Pain từ người khác*) để rà soát quy trình vận hành tại các công ty thành viên Vingroup:

| # | Mảng / Công ty | Tên bài toán | Thấu kính chính (Lens) | Điểm nghẽn lớn nhất (Bottleneck) | Giá trị mang lại khi giải quyết bằng AI |
| :-: | :--- | :--- | :--- | :--- | :--- |
| **01** | 🚗 **VinFast** | Tra cứu Service Manual & Sơ đồ mạch điện | `⏳ Tốn thời gian` | Tài liệu PDF kỹ thuật đồ sộ, KTV mất **20–30 phút/ca** chỉ để tìm đúng trang sơ đồ. | **Cắt giảm 90%** thời gian tra cứu, chuẩn hóa quy trình sửa chữa xe điện toàn cầu. |
| **02** | 🏥 **Vinmec** | Trợ lý ghi bệnh án EMR (Medical Scribe) | `⏳ Tốn thời gian` | Bác sĩ gõ phím **10–15 phút/ca khám**, làm giảm thời gian thăm khám trực tiếp người bệnh. | **Giải phóng 80%** thời gian nhập liệu, giúp bác sĩ tập trung 100% vào chăm sóc bệnh nhân. |
| **03** | 🚕 **Xanh SM** | Thẩm định tranh chấp cuộc gọi / tin nhắn | `🔁 Lặp lại` & `⏳ Tốn thời gian` | Nghe lại hàng trăm phút băng ghi âm và đọc tin nhắn thủ công để bóc tách lỗi vi phạm. | Tự động hóa trích xuất bằng chứng, rút ngắn xử lý tranh chấp từ **20 phút ➔ dưới 3 phút**. |
| **04** | 🏢 **Vinhomes** | Phân luồng & phản hồi ticket cư dân | `⏳ Tốn thời gian` & `⚠️ Pain người khác` | Phân loại và gán thủ công từng yêu cầu sự cố đến các tổ kỹ thuật, gây trễ SLA. | Định tuyến tự động trong **30 giây**, loại bỏ hoàn toàn tình trạng ticket bị chuyển nhầm tổ. |
| **05** | 🎢 **Vinpearl** | Concierge ảo đa kênh In-room / Resort | `⚡ AI nâng cấp` | Tổng đài lễ tân quá tải mùa cao điểm, khách quốc tế bất đồng ngôn ngữ khi gọi hỗ trợ. | Phục vụ **24/7 tức thì đa ngôn ngữ** (Việt, Anh, Hàn, Trung), tự động hóa đặt lịch dịch vụ. |

---

# 🃏 Phase 2 — QUICK-ASSESS: Top 3 Quick Problem Cards

---

### 📋 QUICK PROBLEM CARD #01 — VinFast: Tra cứu Service Manual & Sơ đồ mạch điện

> **Bài toán (1 câu):** Kỹ thuật viên mất quá nhiều thời gian tra cứu tài liệu *Service Manual* PDF hàng nghìn trang để tìm sơ đồ tháo lắp, vị trí linh kiện và mã lỗi xe điện.

* **Công ty thành viên:**
  - [x] **VinFast** &nbsp;&nbsp;&nbsp;&nbsp; [ ] Xanh SM &nbsp;&nbsp;&nbsp;&nbsp; [ ] Vinhomes &nbsp;&nbsp;&nbsp;&nbsp; [ ] Vinmec &nbsp;&nbsp;&nbsp;&nbsp; [ ] Khác

* **Ai đang đau (Actor)?** 
  - Kỹ thuật viên (KTV) xưởng dịch vụ & Cố vấn kỹ thuật sửa chữa.

* **Workflow thủ công hiện tại (5 bước):**
  ```text
  [B1. Cắm máy chẩn đoán DTC] ──▶ [B2. Mở file PDF dòng xe] ──▶ [B3. Tra cứu sơ đồ/mạch] ──▶ [B4. Thao tác trên xe] ──▶ [B5. Kiểm tra & xóa lỗi]
  ```
  1. Cắm máy chẩn đoán đọc mã lỗi (DTC) từ xe.
  2. Mở máy tính tìm file *Service Manual* / *Wiring Diagram* PDF theo đúng dòng & đời xe.
  3. Lật từng trang / `Ctrl+F` tra cứu sơ đồ mạch điện và hướng dẫn tháo lắp chi tiết.
  4. Thao tác xử lý trực tiếp trên xe.
  5. Kiểm tra lại và xóa mã lỗi.

* **Bước nào tốn thời gian / dễ lỗi nhất?**
  - 🔴 **Bước 3** *(⏱ 20 - 30 phút/lượt tra cứu tài liệu)*.

* **AI có thể nhảy vào hỗ trợ ở bước nào?**
  - 🟢 **Bước 2 & 3:** KTV chỉ cần nhập mã lỗi hoặc chụp ảnh/hỏi giọng nói, AI Agent truy vấn RAG sơ đồ kỹ thuật và trích xuất đúng trang/bước cần thao tác.

* **Đo thành công bằng gì (Metric có số)?**
  - ⚡ **Thời gian tra cứu:** Giảm từ **25 phút ──▶ dưới 2 phút/lượt**.
  - 🎯 **Chất lượng:** Tăng tỷ lệ sửa chữa đúng ngay lần đầu (*First-Time Fix Rate*) từ **75% ──▶ trên 90%**.

* **Quick Architecture:**
  - [ ] No AI &nbsp;&nbsp;&nbsp;&nbsp; [ ] Rule &nbsp;&nbsp;&nbsp;&nbsp; [ ] LLM &nbsp;&nbsp;&nbsp;&nbsp; [x] **Agent**
  - *(Agentic RAG đa phương thức: Text + Schematics/Diagram OCR)*

---

### 📋 QUICK PROBLEM CARD #02 — Vinmec: Trợ lý ghi bệnh án EMR (Medical Scribe)

> **Bài toán (1 câu):** Bác sĩ mất nhiều thời gian gõ phím nhập liệu bệnh án EMR và viết tóm tắt điều trị thủ công sau mỗi ca khám, làm giảm thời gian tương tác với bệnh nhân.

* **Công ty thành viên:**
  - [ ] VinFast &nbsp;&nbsp;&nbsp;&nbsp; [ ] Xanh SM &nbsp;&nbsp;&nbsp;&nbsp; [ ] Vinhomes &nbsp;&nbsp;&nbsp;&nbsp; [x] **Vinmec** &nbsp;&nbsp;&nbsp;&nbsp; [ ] Khác

* **Ai đang đau (Actor)?** 
  - Bác sĩ phòng khám ngoại trú / Bác sĩ điều trị nội trú.

* **Workflow thủ công hiện tại (4 bước):**
  ```text
  [B1. Tiếp đón & vấn đáp bệnh sử] ──▶ [B2. Ghi nháp chỉ số & kết luận] ──▶ [B3. Gõ phím nhập liệu EMR] ──▶ [B4. Kê đơn & in phiếu]
  ```
  1. Tiếp đón và vấn đáp bệnh sử, triệu chứng lâm sàng với người bệnh.
  2. Ghi chép nhanh ra giấy nháp các chỉ số và kết luận chẩn đoán.
  3. Ngồi gõ phím nhập liệu chi tiết vào các trường trên phần mềm EMR & tóm tắt phác đồ điều trị.
  4. Kê đơn thuốc, in phiếu và hướng dẫn người bệnh.

* **Bước nào tốn thời gian / dễ lỗi nhất?**
  - 🔴 **Bước 3** *(⏱ 10 - 15 phút/ca bệnh nhân)*.

* **AI có thể nhảy vào hỗ trợ ở bước nào?**
  - 🟢 **Bước 2 & 3:** *Ambient AI Medical Scribe* — Lắng nghe hội thoại bác sĩ - bệnh nhân, tự trích xuất thông tin chuẩn SOAP, điền vào EMR để bác sĩ chỉ cần kiểm tra và bấm duyệt.

* **Đo thành công bằng gì (Metric có số)?**
  - ⚡ **Thời gian hoàn thành EMR:** Giảm từ **12 phút ──▶ dưới 2 phút/ca khám**.
  - 🎯 **Tương tác người bệnh:** Tăng thời gian bác sĩ giao tiếp và thăm khám trực tiếp người bệnh thêm **35% - 40%**.

* **Quick Architecture:**
  - [ ] No AI &nbsp;&nbsp;&nbsp;&nbsp; [ ] Rule &nbsp;&nbsp;&nbsp;&nbsp; [x] **LLM** &nbsp;&nbsp;&nbsp;&nbsp; [ ] Agent
  - *(Speech-to-Text y khoa + LLM trích xuất cấu trúc dữ liệu JSON/SOAP)*

---

### 📋 QUICK PROBLEM CARD #03 — Xanh SM: Thẩm định tranh chấp cuộc gọi / tin nhắn

> **Bài toán (1 câu):** Nhân viên vận hành phải nghe lại thủ công hàng nghìn phút ghi âm cuộc gọi và đọc tin nhắn chat để phân định trách nhiệm khi phát sinh tranh chấp khách - tài.

* **Công ty thành viên:**
  - [ ] VinFast &nbsp;&nbsp;&nbsp;&nbsp; [x] **Xanh SM** &nbsp;&nbsp;&nbsp;&nbsp; [ ] Vinhomes &nbsp;&nbsp;&nbsp;&nbsp; [ ] Vinmec &nbsp;&nbsp;&nbsp;&nbsp; [ ] Khác

* **Ai đang đau (Actor)?** 
  - Chuyên viên CSKH & Nhân viên Vận hành / Giải quyết khiếu nại (Ops/Trust).

* **Workflow thủ công hiện tại (5 bước):**
  ```text
  [B1. Tiếp nhận ticket tranh chấp] ──▶ [B2. Tải ghi âm & chat log] ──▶ [B3. Nghe & đối chiếu dữ liệu] ──▶ [B4. Tra cứu SOP chế tài] ──▶ [B5. Soạn kết luận phản hồi]
  ```
  1. Tiếp nhận ticket phản ánh vi phạm/tranh chấp từ app của khách hoặc tài xế.
  2. Truy xuất ID chuyến đi, tải file ghi âm cuộc gọi và lịch sử tin nhắn nội bộ.
  3. Nghe toàn bộ băng ghi âm cuộc gọi, đọc đối chiếu tin nhắn và dữ liệu GPS.
  4. Tra cứu quy tắc ứng xử / SOP để xác định lỗi thuộc về ai và mức độ xử phạt.
  5. Soạn kết luận, gửi phản hồi bồi hoàn/cảnh cáo cho hai bên.

* **Bước nào tốn thời gian / dễ lỗi nhất?**
  - 🔴 **Bước 3** *(⏱ 15 - 20 phút/ticket tranh chấp)*.

* **AI có thể nhảy vào hỗ trợ ở bước nào?**
  - 🟢 **Bước 3 & 4:** Speech-to-Text chuyển cuộc gọi thành text, LLM phân tích ngữ điệu/từ khóa xúc phạm, trích xuất bằng chứng theo mốc giây và gợi ý chế tài theo đúng quy định.

* **Đo thành công bằng gì (Metric có số)?**
  - ⚡ **Thời gian thẩm định:** Giảm từ **20 phút ──▶ dưới 3 phút/ticket**.
  - 🎯 **Tỷ lệ đúng hạn SLA:** Tăng tỷ lệ giải quyết khiếu nại trong hạn cam kết (SLA 2 giờ) từ **65% ──▶ trên 95%**.

* **Quick Architecture:**
  - [ ] No AI &nbsp;&nbsp;&nbsp;&nbsp; [ ] Rule &nbsp;&nbsp;&nbsp;&nbsp; [ ] LLM &nbsp;&nbsp;&nbsp;&nbsp; [x] **Agent**
  - *(Workflow Agent kết hợp STT, phân loại vi phạm LLM và tra cứu SOP quy định)*

---
