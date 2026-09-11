# QUICK PROBLEM CARDS — PHASE 2

## QUICK PROBLEM CARD #1

```text
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #1                                       │
│                                                             │
│ Bài toán: KTV VinFast cần tra cứu nhanh quy trình sửa chữa, │
│ sơ đồ hoặc mã lỗi trong Service Manual.                    │
│ Công ty thành viên: [x] VinFast                            │
│                                                             │
│ Ai đang đau? KTV (mất thời gian tra cứu), Trưởng ca         │
│ (phải hỗ trợ các câu hỏi lặp lại)                           │
│                                                             │
│ Workflow thủ công hiện tại (5 bước):                       │
│   1. KTV tiếp nhận triệu chứng hoặc mã lỗi từ xe            │
│   → 2. Mở nhiều tài liệu Service Manual liên quan           │
│   → 3. Tìm kiếm thủ công theo từ khóa/mã lỗi                │
│   → 4. Đối chiếu sơ đồ, điều kiện áp dụng và phiên bản      │
│   → 5. Ghi lại quy trình và thực hiện kiểm tra               │
│                                                             │
│ Bước nào tốn nhất? Bước 2-4 (⏱ 10 phút/lượt)               │
│ AI có thể nhảy vào hỗ trợ ở bước nào? Bước 2-4             │
│ (Hiểu câu hỏi tự nhiên → RAG tìm đoạn đúng → Trích nguồn)  │
│                                                             │
│ Đo thành công bằng gì (Metric có số)?                      │
│ Giảm thời gian tra cứu từ 10 phút ──> dưới 2 phút/lượt.    │
│                                                             │
│ Quick Architecture: [x] RAG + LLM                         │
│ (Tra cứu tài liệu, trả lời có trích dẫn và link nguồn)     │
└─────────────────────────────────────────────────────────────┘
```

## QUICK PROBLEM CARD #2

```text
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #2                                       │
│                                                             │
│ Bài toán: Bác sĩ Vinmec cần tạo bản tóm tắt bệnh án có cấu  │
│ trúc từ ghi chú khám bệnh và dữ liệu EMR để duyệt nhanh.   │
│ Công ty thành viên: [x] Vinmec                             │
│                                                             │
│ Ai đang đau? Bác sĩ (quá tải giấy tờ), Điều dưỡng/Thư ký    │
│ (nhập liệu lặp lại), Bệnh nhân (chờ lâu hơn)                │
│                                                             │
│ Workflow thủ công hiện tại (5 bước):                       │
│   1. Bác sĩ xem ghi chú khám và dữ liệu EMR                 │
│   → 2. Chọn lọc triệu chứng, chẩn đoán và thuốc             │
│   → 3. Viết lại diễn biến bệnh theo mẫu                     │
│   → 4. Bổ sung kết quả xét nghiệm và hướng điều trị          │
│   → 5. Kiểm tra, chỉnh sửa và ký duyệt                      │
│                                                             │
│ Bước nào tốn nhất? Bước 2-4 (⏱ 15 phút/bệnh án)             │
│ AI có thể nhảy vào hỗ trợ ở bước nào? Bước 2-4              │
│ (Trích xuất EMR → Draft tóm tắt → Cảnh báo dữ liệu thiếu)  │
│                                                             │
│ Đo thành công bằng gì (Metric có số)?                      │
│ Giảm thời gian soạn tóm tắt từ 15 phút ──> dưới 5 phút.    │
│ Tỷ lệ bác sĩ chỉnh sửa bản nháp vẫn đạt trên 95%.           │
│                                                             │
│ Quick Architecture: [x] LLM Feature + Human-in-the-loop   │
│ (AI soạn nháp, bác sĩ kiểm tra và duyệt trước khi lưu)     │
└─────────────────────────────────────────────────────────────┘
```

## QUICK PROBLEM CARD #3

```text
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #3                                       │
│                                                             │
│ Bài toán: Xanh SM cần đánh giá nhanh tranh chấp giữa khách  │
│ hàng và tài xế dựa trên chat, cuộc gọi, GPS và trạng thái   │
│ chuyến đi.                                                 │
│ Công ty thành viên: [x] Xanh SM (GSM)                      │
│                                                             │
│ Ai đang đau? Nhân viên xử lý khiếu nại (quá tải), Khách     │
│ hàng và tài xế (chờ kết luận)                               │
│                                                             │
│ Workflow thủ công hiện tại (5 bước):                       │
│   1. Nhận nội dung khiếu nại từ khách hoặc tài xế            │
│   → 2. Mở và đọc lịch sử chat, transcript cuộc gọi           │
│   → 3. Đối chiếu GPS, thời gian và trạng thái chuyến         │
│   → 4. Tổng hợp bằng chứng thành timeline sự việc            │
│   → 5. Viết đề xuất kết luận và gửi nhân viên duyệt          │
│                                                             │
│ Bước nào tốn nhất? Bước 2-4 (⏱ 20 phút/vụ)                 │
│ AI có thể nhảy vào hỗ trợ ở bước nào? Bước 2-5              │
│ (Tóm tắt dữ liệu → Dựng timeline → Đề xuất kết luận)       │
│                                                             │
│ Đo thành công bằng gì (Metric có số)?                      │
│ Giảm thời gian xử lý một vụ từ 20 phút ──> dưới 7 phút.    │
│ Tăng số vụ xử lý mỗi nhân viên mỗi ngày thêm 30%.           │
│                                                             │
│ Quick Architecture: [x] LLM Feature + Workflow             │
│ (Tổng hợp đa nguồn, đề xuất kết luận để nhân viên duyệt)   │
└─────────────────────────────────────────────────────────────┘
```
