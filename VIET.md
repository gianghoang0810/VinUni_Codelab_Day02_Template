# Problem Scan — Vin Smart Future (Nguyễn Văn Quốc Việt)

> **Bài làm cá nhân Phase 1 (SCAN) & Phase 2 (QUICK-ASSESS) — Lab 02: AI Product Scoping.**
>
> * **Mục tiêu:** Quét qua vận hành của các công ty thành viên Vingroup bằng **4 Lenses** để tìm ra các bài toán thực tế có thể tối ưu bằng AI.
> * **Mảng kinh doanh đã quét:** **Vinpearl / VinWonders, Xanh SM, Vinhomes, Vinmec.**

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

# 🃏 Phase 2 — QUICK-ASSESS: 3 Quick Problem Cards (Cá nhân)

Chọn top 3 từ danh sách SCAN: **#1 (Vinpearl/VinWonders Chatbot CSKH), #2 (Vinpearl/VinWonders Đào tạo thời vụ), #4 (Vinhomes Năng lượng HVAC).**

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

# 🏗️ Phase 3 — DEEP-DIVE (Nhóm)

Bài toán lựa chọn: **Xanh SM — Phát hiện tài xế câu giờ, không tuân thủ điểm đón, ép khách tự hủy chuyến.**

## 3.3. Future-State Flow & AI Fit

* **AI Fit:** Chọn **Rule + LLM Feature (Hybrid)**. Quick Card ban đầu chọn LLM, nhưng khi phân tích sâu, phần phát hiện "xe đứng yên / đi sai hướng" là tín hiệu số từ GPS nên dùng **Rule** sẽ nhanh, rẻ và chính xác hơn. **LLM** chỉ dùng cho phần Rule không làm được: hiểu hội thoại tiếng Việt để bắt các câu ép khách tự hủy và soạn hồ sơ bằng chứng. **Không dùng Agent** vì quyết định xử lý tài xế ảnh hưởng trực tiếp đến thu nhập của họ, bắt buộc phải có con người duyệt.

| Tiêu chí | Rule / State-Machine | LLM Feature | Agentic Loop |
|---|---|---|---|
| Phát hiện xe đứng yên, đi sai hướng qua GPS | ✅ Tốt nhất (ngưỡng khoảng cách, tốc độ, hướng) | ❌ Không cần thiết | ❌ Quá mức cần thiết |
| Hiểu hội thoại *"xa quá, bạn hủy giúp mình nhé"* | ❌ Bắt keyword dễ sót / nhầm | ✅ Hiểu ngữ cảnh, cách nói lóng | ⚠️ Làm được nhưng thừa |
| Soạn tóm tắt hồ sơ bằng chứng | ❌ Không làm được | ✅ Phù hợp | ⚠️ Thừa |
| Tự ra quyết định phạt tài xế | ⛔ Cấm | ⛔ Cấm | ⛔ Cấm — rủi ro cao nhất |
| Chi phí & độ trễ | Rất thấp, real-time | Trung bình, vài giây | Cao, khó kiểm soát |
| **Kết luận** | **Dùng cho Bước 1-2** | **Dùng cho Bước 3-4** | **Không dùng** |

* **Quy trình tương lai (Future-State):**

```text
┌──────────────────┐     ┌──────────────────┐     ┌──────────────────┐     ┌──────────────────┐
│ Bước 1           │     │ Bước 2           │     │ Bước 3           │     │ Bước 4           │
│ 🟡 Rule giám sát │     │ 🟡 Cảnh báo sớm: │     │ 🔵 LLM phân tích │     │ 🔵 AI soạn hồ sơ │
│ GPS sau khi tài  │ ──→ │ nhắc tài xế,     │ ──→ │ hội thoại, bắt   │ ──→ │ bằng chứng       │
│ xế nhận cuốc     │     │ cho khách đổi xe │     │ câu ép tự hủy    │     │ [DRAFT_ONLY]     │
│                  │     │                  │     │                  │     │                  │
│ Ai: Hệ thống     │     │ Ai: Hệ thống     │     │ Ai: LLM          │     │ Ai: LLM          │
│ Real-time        │     │ Real-time        │     │ ~10 giây         │     │ ~5 giây          │
└──────────────────┘     └──────────────────┘     └──────────────────┘     └──────────────────┘
                                                                                     │
                                                                                     ▼
                                                                           ┌──────────────────┐
                                                                           │ Bước 5           │
                                                                           │ 🟢 Vận hành      │
                                                                           │ duyệt & ra quyết │
                                                                           │ định xử lý       │
                                                                           │                  │
                                                                           │ Ai: Nhân viên    │
                                                                           │ < 1 phút         │
                                                                           └──────────────────┘

↩️ Fallback:
  • LLM lỗi / timeout / JSON sai định dạng / confidence < 0.7
    → hồ sơ gắn nhãn "Cần review thủ công", nhân viên xử lý như quy trình cũ.
  • GPS mất tín hiệu (hầm, bãi xe trong tòa nhà) → KHÔNG gắn cờ tự động.
  • Chuyến không có hội thoại → chỉ dùng bằng chứng GPS, nhân viên quyết định.

🟡 = Rule step (tất định)   🔵 = AI step (LLM)   🟢 = Human step (HITL)
⏱ Tổng thời gian xác minh: 10-15 phút ──> dưới 1 phút/lượt.
```

### Chi tiết các bước

| Bước | Loại | Input | Xử lý | Output |
|---|---|---|---|---|
| **1** | 🟡 Rule | Luồng GPS của xe, tọa độ điểm đón, thời điểm nhận cuốc | Gắn cờ khi: xe đứng yên > 3 phút; **hoặc** khoảng cách tới điểm đón không giảm sau 5 phút; **hoặc** đi ngược hướng điểm đón > 500 m | Cờ `suspected_stalling` + GPS timeline |
| **2** | 🟡 Rule | Cờ từ Bước 1 | Gửi nhắc nhở cho tài xế qua App; sau 2 phút vẫn vi phạm → hiện cho khách tùy chọn **đổi tài xế, miễn phí hủy** | Khách được đổi xe thay vì phải chờ hoặc tự hủy |
| **3** | 🔵 LLM | Log chat trong App + transcript cuộc gọi (đã ẩn SĐT) — kích hoạt khi khách hủy/khiếu nại hoặc chuyến bị gắn cờ | Phát hiện câu ép hủy, viện cớ, hẹn lấy khách ngoài App | JSON `{violation_type, confidence, quotes[]}` |
| **4** | 🔵 LLM | GPS timeline + kết quả Bước 3 | Soạn tóm tắt hồ sơ vi phạm, đề xuất phân loại theo chính sách xử lý tài xế | Hồ sơ `[DRAFT_ONLY]` kèm trích dẫn nguyên văn và timestamp |
| **5** | 🟢 Human | Hồ sơ nháp từ Bước 4 | Nhân viên Vận hành xác nhận hoặc bác bỏ, ra quyết định xử lý | Quyết định chính thức + phản hồi cho khách |

### Operational Boundary (Ranh giới vận hành)

* ✅ **AI được phép:** đọc log chat / transcript của **đúng chuyến** bị gắn cờ; phân loại hành vi; tóm tắt bằng chứng; đề xuất mức vi phạm.
* ⛔ **AI tuyệt đối không được:** tự động phạt, trừ tiền hay khóa tài khoản tài xế; đưa ra kết luận khi không có trích dẫn nguyên văn hoặc timestamp GPS làm bằng chứng; đưa thông tin cá nhân (SĐT, địa chỉ nhà) vào hồ sơ.
* 🟢 **Bắt buộc con người duyệt (HITL):** mọi quyết định xử lý tài xế do nhân viên Vận hành ra. Tài xế luôn có quyền khiếu nại quyết định.

### Liên kết với Success Metric

| Metric | Bước tạo ra tác động |
|---|---|
| Thời gian xác minh lỗi hủy chuyến / câu giờ: 10-15 phút ──> **dưới 1 phút** | Bước 3-4: nhân viên nhận hồ sơ đã tổng hợp sẵn, chỉ cần duyệt thay vì tự nghe lại hội thoại và dò GPS |
| Giảm **15%** tỷ lệ khách tự hủy do chờ lâu | Bước 1-2: phát hiện sớm và cho khách đổi xe **ngay trong chuyến**, trước khi khách bỏ cuộc |
