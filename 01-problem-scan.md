# 01 — Problem Scan: Vin Smart Future (Nguyễn Văn Quốc Việt)

> **Bài làm Phase 1 (SCAN) & Phase 2 (QUICK-ASSESS) — Lab 02: AI Product Scoping.**
>
> * **Mục tiêu:** Quét qua vận hành của các công ty thành viên Vingroup bằng **4 Lenses** để tìm ra các bài toán thực tế có thể tối ưu bằng AI, sau đó đánh giá nhanh các bài toán tiềm năng nhất.
> * **Mảng kinh doanh đã quét:** **Vinpearl / VinWonders, Xanh SM, Vinhomes, Vinmec.**
> * **Bài toán được chọn để Deep-Dive:** **Xanh SM — Phát hiện tài xế câu giờ / ép khách tự hủy (Card #3).**

---

# 🔍 Phase 1 — SCAN: Tìm kiếm cơ hội (Cá nhân)

Dùng **4 Lenses** quét qua vận hành của các công ty thành viên Vingroup.

| # | Subsidiary | Lens | Mô tả ngắn bài toán |
|---|------------|------|---------------------|
| 1 | **Vinpearl / VinWonders** | AI có thể tốt hơn | Chatbot CSKH trả lời rập khuôn theo kịch bản, không cá nhân hóa theo loại khách (gia đình, cặp đôi, đoàn), không đặt vé trực tiếp được trong hội thoại. |
| 2 | **Vinpearl / VinWonders** | Tốn thời gian | Mỗi mùa cao điểm tuyển hàng trăm nhân viên thời vụ, đào tạo lặp lại quy trình/SOP bằng hình thức lớp học truyền thống, tốn thời gian quản lý. |
| 3 | **Xanh SM** | Pain từ người khác | Khách phải chờ lâu hoặc hủy chuyến khi tài xế đã nhận cuốc nhưng đứng yên, đi sai hướng hoặc không chủ động di chuyển về điểm đón. |
| 4 | **Vinhomes** | AI có thể tốt hơn | Lãng phí năng lượng điện/HVAC tại các khu vực tiện ích chung (Sảnh, NSHCĐ, Hành lang) do bật/tắt theo lịch cứng thay vì theo lưu lượng thực tế. |
| 5 | **Vinmec** | AI có thể tốt hơn | Lập lịch và điều phối công suất phòng mổ bằng spreadsheet tĩnh, không tối ưu được thời gian dọn phòng/khử khuẩn thực tế hay độ biến thiên theo thể trạng bệnh nhân. |

---

# 🃏 Phase 2 — QUICK-ASSESS: Quick Problem Cards (Cá nhân)

Hoàn thiện Quick Problem Cards cho các bài toán tiềm năng nhất từ danh sách SCAN: **#1 (Vinpearl/VinWonders Chatbot CSKH), #2 (Vinpearl/VinWonders Đào tạo thời vụ), #3 (Xanh SM Tài xế câu giờ / ép khách tự hủy), #4 (Vinhomes Năng lượng HVAC).**

## Card #1 — Vinpearl / VinWonders: Chatbot CSKH cá nhân hóa & đặt vé trong hội thoại

```text
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #1                                       │
│                                                             │
│ Bài toán: Chatbot CSKH Vinpearl/VinWonders trả lời rập      │
│ khuôn theo kịch bản, không cá nhân hóa theo loại khách,     │
│ không đặt vé trực tiếp được trong hội thoại.                │
│ Công ty thành viên: [x] Khác: Vinpearl / VinWonders         │
│                                                             │
│ Ai đang đau? Khách hàng (hỏi mãi không ra gói phù hợp),     │
│ Nhân viên CSKH/tổng đài (tiếp nhận lại ca chatbot bỏ dở)    │
│                                                             │
│ Workflow thủ công hiện tại (5 bước):                        │
│   1. Khách hỏi chatbot về vé, combo, lịch trình             │
│   → 2. Chatbot trả lời theo kịch bản, gửi link chung        │
│   → 3. Không ra gói phù hợp → khách gọi tổng đài            │
│   → 4. Nhân viên hỏi lại nhu cầu, tư vấn gói, hướng dẫn     │
│        đặt vé trên web/app                                  │
│   → 5. Khách tự đặt vé và thanh toán trên web/app           │
│                                                             │
│ Bước nào tốn nhất? Bước 3-4 (~12 phút/lượt)                 │
│ AI có thể nhảy vào hỗ trợ ở bước nào? Bước 2-4              │
│ (Hiểu nhu cầu theo loại khách → gợi ý gói → tạo đơn         │
│ đặt vé nháp ngay trong hội thoại để khách xác nhận)         │
│                                                             │
│ Đo thành công bằng gì (Metric có số)?                       │
│ Tỉ lệ chatbot tự xử lý trọn vẹn (không chuyển nhân viên)    │
│ tăng từ ~30% ──> 70%; thời gian từ lúc hỏi đến lúc đặt      │
│ vé giảm từ ~15 phút ──> dưới 5 phút.                        │
│                                                             │
│ Quick Architecture: [x] LLM Feature (gọi API giá/đặt vé)    │
└─────────────────────────────────────────────────────────────┘
```

---

## Card #2 — Vinpearl / VinWonders: Đào tạo SOP cho nhân viên thời vụ

```text
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #2                                       │
│                                                             │
│ Bài toán: Mỗi mùa cao điểm, Vinpearl/VinWonders đào tạo     │
│ SOP lặp lại cho hàng trăm nhân viên thời vụ bằng lớp học    │
│ truyền thống, tốn thời gian của quản lý.                    │
│ Công ty thành viên: [x] Khác: Vinpearl / VinWonders         │
│                                                             │
│ Ai đang đau? Trainer/Quản lý bộ phận (dạy lại từ đầu mỗi    │
│ đợt, bị hỏi lại liên tục), Nhân viên thời vụ (học dồn)      │
│                                                             │
│ Workflow thủ công hiện tại (4 bước):                        │
│   1. HR tuyển nhân viên thời vụ theo đợt                    │
│   → 2. Trainer dạy SOP trên lớp (vận hành trò chơi, an      │
│        toàn, CSKH) - 2 ngày/đợt                             │
│   → 3. Kiểm tra trên giấy, trainer chấm tay                 │
│   → 4. Vào ca gặp tình huống lạ → hỏi lại quản lý ca        │
│                                                             │
│ Bước nào tốn nhất? Bước 2 (16 giờ lớp/đợt) và Bước 4        │
│ (~5-10 phút/câu hỏi, 20-30 câu/ca cho mỗi quản lý)          │
│ AI có thể nhảy vào hỗ trợ ở bước nào? Bước 2-4              │
│ (Trợ lý SOP hỏi-đáp tức thì trong ca, trích dẫn đúng mục    │
│ SOP; tự sinh quiz theo vị trí; trainer chỉ dạy thực hành)   │
│                                                             │
│ Đo thành công bằng gì (Metric có số)?                       │
│ Giảm giờ học lý thuyết từ 16 giờ ──> 6 giờ/nhân viên;       │
│ giảm 60% câu hỏi lặp lại gửi lên quản lý ca.                │
│                                                             │
│ Quick Architecture: [x] LLM Feature (RAG trên tài liệu SOP) │
└─────────────────────────────────────────────────────────────┘
```

---

## Card #3 — Xanh SM: Phát hiện tài xế câu giờ, không tuân thủ điểm đón, ép khách tự hủy

```text
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #3                                       │
│                                                             │
│ Bài toán: Hệ thống không tự động phát hiện được tài xế      │
│ câu giờ, không tuân thủ điểm đón, ép khách tự hủy chuyến.   │
│ Công ty thành viên: [x] Xanh SM                             │
│                                                             │
│ Ai đang đau? Khách hàng (chờ lâu), Nhân viên Vận hành       │
│ (xác minh thủ công từng vụ)                                 │
│                                                             │
│ Workflow thủ công hiện tại (4 bước):                        │
│   1. Khách hàng phàn nàn/khiếu nại hoặc tự hủy chuyến       │
│   → 2. Vận hành/CSKH mở lịch sử chuyến đi và định vị GPS    │
│   → 3. Đọc/nghe lại hội thoại giữa khách hàng và tài xế     │
│   → 4. Phân loại vi phạm, đối chiếu bằng chứng để ra QĐ     │
│                                                             │
│ Bước nào tốn nhất? Bước 3-4 (10-15 phút/lượt)               │
│ AI có thể nhảy vào hỗ trợ ở bước nào? Bước 3-4              │
│ (Tự động phân tích hội thoại, phát hiện hành vi trì hoãn,   │
│ cung cấp bằng chứng để nhân viên ra quyết định nhanh)       │
│                                                             │
│ Đo thành công bằng gì (Metric có số)?                       │
│ Giảm thời gian xác minh lỗi hủy chuyến/câu giờ xuống        │
│ dưới 1 phút; giảm 15% tỷ lệ khách tự hủy do chờ lâu.        │
│                                                             │
│ Quick Architecture: [x] LLM Feature                         │
└─────────────────────────────────────────────────────────────┘
```

---

## Card #4 — Vinhomes: Điều khiển điện/HVAC tiện ích chung theo lưu lượng thực tế

```text
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #4                                       │
│                                                             │
│ Bài toán: Điện/HVAC tại tiện ích chung (Sảnh, NSHCĐ, Hành   │
│ lang) bật/tắt theo lịch cứng thay vì theo lưu lượng người   │
│ thực tế, gây lãng phí năng lượng.                           │
│ Công ty thành viên: [x] Vinhomes                            │
│                                                             │
│ Ai đang đau? Ban Quản lý & Kỹ thuật vận hành tòa nhà (chi   │
│ phí điện cao, phải chỉnh tay), Cư dân (gánh phí dịch vụ)    │
│                                                             │
│ Workflow thủ công hiện tại (4 bước):                        │
│   1. Kỹ thuật cài lịch cố định trên BMS (VD: 5h30-23h)      │
│   → 2. HVAC/đèn chạy theo lịch dù khu vực vắng người        │
│   → 3. Cư dân phản ánh nóng/lạnh → kỹ thuật chỉnh tay       │
│   → 4. Cuối tháng đối chiếu hóa đơn điện bằng Excel, sửa    │
│        lịch theo cảm tính                                   │
│                                                             │
│ Bước nào lãng phí nhất? Bước 2 (chạy khi vắng người         │
│ ~30-40% thời gian) và Bước 4 (~4 giờ/tháng/tòa)             │
│ AI có thể nhảy vào hỗ trợ ở bước nào? Bước 1-2              │
│ (Đếm người từ camera/cảm biến/thẻ ra vào → dự báo lưu       │
│ lượng theo giờ → đề xuất lịch chạy & setpoint phù hợp)      │
│                                                             │
│ Đo thành công bằng gì (Metric có số)?                       │
│ Giảm 20-25% điện năng HVAC & chiếu sáng khu vực chung;      │
│ nhiệt độ sảnh giữ trong 24-27°C, phản ánh không tăng.       │
│                                                             │
│ Quick Architecture: [x] Rule (cảm biến hiện diện) + ML      │
│ dự báo lưu lượng — không cần LLM                            │
└─────────────────────────────────────────────────────────────┘
```

---

# 🗳️ Quyết định lựa chọn của nhóm:
Nhóm quyết định chọn bài toán **"Card #3 — Xanh SM: Phát hiện tài xế câu giờ, không tuân thủ điểm đón, ép khách tự hủy"** để thực hiện Deep-Dive (xem [02-deep-dive-report.md](02-deep-dive-report.md)).

## Lý do lựa chọn Card #3:
* **Tác động trực tiếp, real-time:** Ảnh hưởng ngay đến trải nghiệm khách hàng đang chờ xe và doanh thu mỗi cuốc, không chỉ là tác vụ back-office.
* **Dữ liệu đã có sẵn:** Log GPS, trạng thái cuốc xe và chat in-app đều đã được hệ thống Xanh SM ghi lại — không cần đầu tư phần cứng mới.
* **Metric rõ ràng, đo được:** Thời gian xác minh (10-15 phút ──> dưới 1 phút) và tỷ lệ khách tự hủy do chờ lâu (giảm 15%).
* **Rủi ro kiểm soát được:** AI chỉ tạo hồ sơ nháp, mọi quyết định xử lý tài xế đều do nhân viên duyệt (HITL).

## Lý do loại bỏ các thẻ khác:
* **Card #1 (Vinpearl Chatbot CSKH):** Đặt vé ngay trong hội thoại đòi hỏi tích hợp sâu với hệ thống booking và thanh toán; rủi ro báo sai giá hoặc đặt nhầm vé ảnh hưởng trực tiếp đến tiền của khách. Phạm vi quá lớn cho vòng đầu.
* **Card #2 (Vinpearl Đào tạo thời vụ):** Giá trị chỉ tập trung vào mùa cao điểm nên khó đo hiệu quả nhanh; cần số hóa và chuẩn hóa toàn bộ kho tài liệu SOP trước khi làm AI.
* **Card #4 (Vinhomes HVAC):** Bài toán cốt lõi là cảm biến IoT và mô hình dự báo, không phải LLM; phụ thuộc vào đầu tư phần cứng và khả năng tích hợp hệ thống BMS của từng tòa nhà.
