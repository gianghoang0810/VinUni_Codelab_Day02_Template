# Lab 02 — Worksheet: AI Product Scoping
**Người thực hiện:** Đinh Mạnh Dũng (DinhManhDung)

---

# 🔍 Phase 1 — SCAN (Cá nhân)

### 📝 List bài toán của tôi:
| # | Subsidiary | Lens | Mô tả ngắn bài toán |
|---|------------|------|---------------------|
| 1 | **VinFast** (Hậu mãi) | Tốn thời gian | Kỹ thuật viên bảo hành tốn 20-30 phút lật giở tài liệu PDF/Service Manuals hàng ngàn trang để tìm đúng sơ đồ tháo lắp pin hoặc reset cảm biến, làm kéo dài thời gian sửa chữa. |
| 2 | **Xanh SM** | Pain từ người khác | Khách hàng phàn nàn vì tài xế câu giờ, không tuân thủ điểm đón, bắt khách tự hủy chuyến. Nhân viên CSKH/Vận hành mất nhiều thời gian kiểm tra chất lượng và xử lý khiếu nại. |
| 3 | **Vinpearl / VinWonders** | Tốn thời gian | Mỗi mùa cao điểm phải tuyển hàng trăm nhân viên thời vụ, tốn nhiều thời gian quản lý và đào tạo lặp lại các quy trình/SOP bằng hình thức lớp học truyền thống. |
| 4 | **Vinhomes** | Tốn thời gian | Nhân sự Ban quản lý tốn nhiều thời gian đối soát thủ công hàng nghìn hóa đơn điện, nước, phí dịch vụ mỗi tháng, dễ xảy ra sai sót dữ liệu. |
| 5 | **Vinmec** | Pain từ người khác | Nút thắt quy trình xuất viện rời rạc khiến bệnh nhân chờ đợi lâu (4-6 tiếng), gây ứ đọng giường bệnh cấp cứu và giảm hiệu suất luân chuyển giường. |
| 6 | **VinFast** (Sản xuất) | AI-upgrade | Hệ thống HVAC, lò sấy và máy dập vận hành theo công suất cố định hoặc thủ công, gây lãng phí điện và tăng phụ tải đỉnh. |

---

# 🃏 Phase 2 — QUICK-ASSESS (Cá nhân)

Dưới đây là 3 thẻ bài toán (Quick Problem Cards) tiêu biểu được chọn lọc từ danh sách trên:

```text
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #1                                       │
│                                                             │
│ Bài toán (1 câu): Kỹ thuật viên tốn nhiều thời gian tra cứu │
│ tài liệu sửa chữa (PDF) để tìm sơ đồ và hướng dẫn tháo lắp. │
│ Công ty thành viên: [x] VinFast  [ ] Xanh SM  [ ] Vinhomes  │
│                     [ ] Vinmec   [ ] Khác (Ghi rõ)________  │
│                                                             │
│ Ai đang đau (Actor)? Kỹ thuật viên (KTV), Khách hàng        │
│                                                             │
│ Workflow thủ công hiện tại (4 bước):                        │
│   1. KTV nhận xe và chẩn đoán mã lỗi (VD: B1001)            │
│   ──> 2. Mở file PDF Service Manuals hàng ngàn trang        │
│   ──> 3. Tìm kiếm thủ công mã lỗi hoặc bộ phận cần sửa      │
│   ──> 4. Đọc, xác định các bước thực hiện và sơ đồ mạch điện│
│                                                             │
│ Bước nào tốn thời gian/lỗi nhất? Bước 2-3 (⏱ 20-30 phút/lượt)
│ AI có thể nhảy vào hỗ trợ ở bước nào? Bước 2-4 (RAG Chatbot │
│ hỗ trợ KTV hỏi "Cách tháo cụm đèn pha VF 8 mã lỗi B1001" và │
│ tự động trích xuất tài liệu, sơ đồ, tóm tắt các bước).      │
│                                                             │
│ Đo thành công bằng gì (Metric có số)?                       │
│ Giảm thời gian tra cứu tài liệu từ 20-30 phút ──> dưới 1 phút.
│                                                             │
│ Quick Architecture: [ ] No AI  [ ] Rule  [x] LLM  [ ] Agent │
└─────────────────────────────────────────────────────────────┘
```

```text
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #2                                       │
│                                                             │
│ Bài toán (1 câu): Hệ thống không tự động phát hiện được     │
│ tài xế câu giờ, không tuân thủ điểm đón ép khách tự hủy.    │
│ Công ty thành viên: [ ] VinFast  [x] Xanh SM  [ ] Vinhomes  │
│                     [ ] Vinmec   [ ] Khác (Ghi rõ)________  │
│                                                             │
│ Ai đang đau (Actor)? Khách hàng (chờ lâu), Nhân viên Vận hành
│                                                             │
│ Workflow thủ công hiện tại (4 bước):                        │
│   1. Khách hàng phàn nàn/khiếu nại hoặc tự hủy chuyến       │
│   ──> 2. Vận hành/CSKH mở lịch sử chuyến đi và định vị GPS  │
│   ──> 3. Đọc/Nghe lại hội thoại giữa khách hàng và tài xế   │
│   ──> 4. Phân loại vi phạm, đối chiếu bằng chứng để ra QĐ   │
│                                                             │
│ Bước nào tốn thời gian/lỗi nhất? Bước 3-4 (⏱ 10-15 phút/lượt)
│ AI có thể nhảy vào hỗ trợ ở bước nào? Bước 3-4 (Tự động phân│
│ tích hội thoại, phát hiện hành vi trì hoãn, cung cấp bằng   │
│ chứng để nhân viên ra quyết định nhanh chóng).              │
│                                                             │
│ Đo thành công bằng gì (Metric có số)?                       │
│ Giảm thời gian xác minh lỗi hủy chuyến/câu giờ xuống dưới 1 │
│ phút, giảm 15% tỷ lệ khách tự hủy do chờ lâu.               │
│                                                             │
│ Quick Architecture: [ ] No AI  [ ] Rule  [x] LLM  [ ] Agent │
└─────────────────────────────────────────────────────────────┘
```

```text
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #3                                       │
│                                                             │
│ Bài toán (1 câu): Quy trình xuất viện rời rạc khiến bệnh    │
│ nhân phải chờ đợi lâu (4-6 tiếng), gây ứ đọng giường bệnh.  │
│ Công ty thành viên: [ ] VinFast  [ ] Xanh SM  [ ] Vinhomes  │
│                     [x] Vinmec   [ ] Khác (Ghi rõ)________  │
│                                                             │
│ Ai đang đau (Actor)? Bệnh nhân, Bác sĩ/Điều dưỡng, Bệnh viện│
│                                                             │
│ Workflow thủ công hiện tại (4 bước):                        │
│   1. Bác sĩ ra y lệnh xuất viện, tổng hợp tóm tắt bệnh án   │
│   ──> 2. Chuyển hồ sơ sang khoa Dược để chốt thuốc          │
│   ──> 3. Chuyển sang Kế toán để chốt viện phí và bảo hiểm   │
│   ──> 4. Thông báo bệnh nhân thanh toán và nhận giấy tờ     │
│                                                             │
│ Bước nào tốn thời gian/lỗi nhất? Bước 1 & 3 (⏱ 4-6 tiếng)   │
│ AI có thể nhảy vào hỗ trợ ở bước nào? Bước 1 & 3 (AI tự động│
│ tóm tắt bệnh án xuất viện và hỗ trợ đối soát bảo hiểm/phí). │
│                                                             │
│ Đo thành công bằng gì (Metric có số)?                       │
│ Rút ngắn tổng thời gian hoàn tất thủ tục xuất viện từ 4-6   │
│ tiếng ──> dưới 1.5 tiếng/lượt.                              │
│                                                             │
│ Quick Architecture: [ ] No AI  [ ] Rule  [x] LLM  [ ] Agent │
└─────────────────────────────────────────────────────────────┘
```
