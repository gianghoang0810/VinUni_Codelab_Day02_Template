# Đề tài AI đề xuất

| # | Subsidiary | Lens | Mô tả ngắn bài toán |
| --- | --- | --- | --- |
| 1 | Xanh SM | Lặp lại | Nhân viên phải kiểm tra thủ công lý do hủy, vị trí tài xế, thời gian chờ, lịch sử liên hệ và ảnh bằng chứng để xác định chuyến hủy có hợp lệ hay không. |
| 2 | VinFast | Tốn thời gian | KTV mất 20–30 phút lật các file PDF Service Manual để tìm đúng sơ đồ sửa chữa, tháo lắp pin hoặc xử lý mã lỗi. |
| 3 | Vinpearl / VinWonders | AI-upgrade | Trợ lý resort trả lời theo kịch bản, không cá nhân hóa theo loại khách và chưa hỗ trợ đặt dịch vụ trực tiếp trong hội thoại. |
| 4 | Vinhomes | Pain từ người khác | Hệ thống MEP như thang máy, PCCC và máy bơm hỏng đột xuất, gây gián đoạn vận hành và tốn chi phí sửa chữa do thiếu cơ chế dự báo bảo trì. |
| 5 | Vinmec | AI-upgrade | Lập lịch và điều phối công suất phòng mổ bằng spreadsheet tĩnh, không tối ưu được thời gian dọn phòng, khử khuẩn và biến động theo thể trạng bệnh nhân. |

# Quick Problem Cards

```text
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #1                                       │
│                                                             │
│ Bài toán: Tự động xác minh bằng chứng hủy chuyến.           │
│ Công ty thành viên: [x] Xanh SM (GSM)                       │
│                                                             │
│ Ai đang đau? Điều phối viên, tài xế và khách hàng.          │
│                                                             │
│ Workflow thủ công hiện tại (5 bước):                        │
│  1. Nhận yêu cầu/khiếu nại hủy chuyến                       │
│  → 2. Kiểm tra lý do hủy và thời gian chờ                   │
│  → 3. Đối chiếu GPS, vị trí tài xế và lịch sử liên hệ       │
│  → 4. Xem ảnh/chứng cứ nếu có                               │
│  → 5. Kết luận hợp lệ, không hợp lệ hoặc cần kiểm tra       │
│                                                             │
│ Bước nào tốn nhất? Bước 2–4.                                │
│ AI có thể nhảy vào hỗ trợ ở bước nào? Bước 2–4.             │
│ (Tổng hợp GPS, lịch sử chuyến và bằng chứng để đề xuất      │
│ kết luận cho điều phối viên.)                               │
│                                                             │
│ Đo thành công bằng gì? Giảm thời gian xử lý một hồ sơ       │
│ xuống dưới 3 phút; độ chính xác đề xuất từ 90% trở lên.     │
│                                                             │
│ Quick Architecture: [x] Rules + ML/Multimodal Feature       │
└─────────────────────────────────────────────────────────────┘
```

```text
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #2                                       │
│                                                             │
│ Bài toán: Trợ lý AI tra cứu tài liệu sửa chữa cho KTV.      │
│ Công ty thành viên: [x] VinFast                             │
│                                                             │
│ Ai đang đau? KTV mới, quản đốc xưởng và khách hàng chờ xe.  │
│                                                             │
│ Workflow thủ công hiện tại (5 bước):                        │
│  1. KTV nhận mã lỗi hoặc mô tả sự cố                        │
│  → 2. Mở các PDF Service Manual                             │
│  → 3. Tìm thủ công theo dòng xe/mã lỗi                      │
│  → 4. Đọc sơ đồ mạch và quy trình sửa chữa                  │
│  → 5. Thực hiện sửa chữa hoặc hỏi KTV giàu kinh nghiệm      │
│                                                             │
│ Bước nào tốn nhất? Bước 2–4 (⏱ 20–30 phút/lượt).            │
│ AI có thể nhảy vào hỗ trợ ở bước nào? Bước 2–4.             │
│ (Nhập mã lỗi → tìm đúng trang PDF/sơ đồ → tóm tắt bước làm.)│
│                                                             │
│ Đo thành công bằng gì? Giảm thời gian tra cứu từ 20–30 phút │
│ xuống dưới 5 phút/lượt.                                     │
│                                                             │
│ Quick Architecture: [x] RAG + LLM Feature                   │
└─────────────────────────────────────────────────────────────┘
```

```text
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #3                                       │
│                                                             │
│ Bài toán: Dự báo hỏng hóc hệ thống MEP tại khu đô thị.      │
│ Công ty thành viên: [x] Vinhomes                            │
│                                                             │
│ Ai đang đau? Cư dân, ban quản lý và đội bảo trì.            │
│                                                             │
│ Workflow thủ công hiện tại (5 bước):                        │
│  1. Hệ thống MEP phát sinh dấu hiệu bất thường              │
│  → 2. Cư dân/BQL báo sự cố                                  │
│  → 3. Đội kỹ thuật kiểm tra tại hiện trường                 │
│  → 4. Chẩn đoán nguyên nhân và gọi vật tư                   │
│  → 5. Sửa chữa sau khi thiết bị đã hỏng                     │
│                                                             │
│ Bước nào tốn nhất? Bước 3–5, đặc biệt khi sự cố đột xuất.   │
│ AI có thể nhảy vào hỗ trợ ở bước nào? Bước 1–2.             │
│ (Phân tích dữ liệu cảm biến để cảnh báo sớm nguy cơ hỏng.)  │
│                                                             │
│ Đo thành công bằng gì? Giảm ít nhất 30% số sự cố MEP đột    │
│ xuất và tăng tỷ lệ bảo trì chủ động lên trên 70%.           │
│                                                             │
│ Quick Architecture: [x] IoT Time-series ML / Anomaly Detect │
└─────────────────────────────────────────────────────────────┘
```
