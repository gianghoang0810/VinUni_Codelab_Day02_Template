# 02 — Deep-Dive Report: Xanh SM — Phát hiện tài xế câu giờ & ép khách tự hủy

> **Báo cáo Phase 3 (DEEP-DIVE) & Phase 5 (EVALUATE) — Lab 02: AI Product Scoping.**
>
> * **Bài toán:** Hệ thống Xanh SM không tự động phát hiện được tài xế câu giờ, không tuân thủ điểm đón, ép khách tự hủy chuyến (Card #3 trong [01-problem-scan.md](01-problem-scan.md)).
> * **AI Fit:** **Rule + LLM Feature (Hybrid)** — Rule giám sát GPS real-time, LLM phân tích hội thoại và soạn hồ sơ bằng chứng, nhân viên Vận hành duyệt (HITL).
> * **Quyết định:** **GO** — pilot phạm vi hẹp (xem Phase 5).

---

# 🏗️ Phase 3 — DEEP-DIVE (Nhóm)

## 3.1. Current-State Workflow
Quy trình xử lý thủ công hiện tại khi có khiếu nại tài xế câu giờ, không tuân thủ điểm đón hoặc khách tự hủy chuyến:

```text
┌──────────────────────┐     ┌──────────────────────┐     ┌──────────────────────┐     ┌──────────────────────┐
│ Bước 1               │     │ Bước 2               │     │ Bước 3 🔴            │     │ Bước 4 🔴            │
│ Nhận khiếu nại       │     │ Mở lịch sử chuyến    │     │ Đọc chat, nghe lại   │     │ Phân loại vi phạm,   │
│ hoặc ghi nhận        │ ──→ │ và log GPS trên      │ ──→ │ ghi âm, đối chiếu    │ ──→ │ ra quyết định        │
│ khách tự hủy         │ 🔄  │ hệ thống nội bộ      │ 🔄  │ từng mốc GPS         │     │ xử phạt/hoàn phí     │
│                      │     │                      │     │                      │     │                      │
│ Ai: CSKH             │     │ Ai: Vận hành         │     │ Ai: Vận hành         │     │ Ai: Vận hành         │
│ Thời gian: 1 phút    │     │ Thời gian: 2 phút    │     │ Thời gian: 5-7 phút  │     │ Thời gian: 5-8 phút  │
│                      │     │                      │     │                      │     │                      │
│ In: Cuộc gọi, chat   │     │ In: Mã chuyến        │     │ In: Chat, ghi âm     │     │ In: Bằng chứng       │
│ Out: Ticket sự cố    │     │ Out: Lộ trình GPS    │     │ Out: Ghi chú b.chứng │     │ Out: Quyết định      │
└──────────────────────┘     └──────────────────────┘     └──────────────────────┘     └──────────────────────┘
                                                                                                   │
                                                                                                   ▼  🔄 CSKH phản hồi khách & thông báo cho tài xế

🔴 = Bottleneck      🔄 = Handoff (chuyển giao giữa người / bộ phận / hệ thống)
⏱ Tổng thời gian xử lý thủ công: 13-18 phút/lượt (riêng Bước 3-4 chiếm 10-15 phút).
```

### Các điểm Handoff 🔄

| # | Handoff | Vấn đề gây ra |
|---|---|---|
| **H1** | Khách hàng → CSKH → Vận hành (chuyển ticket) | Ticket thường thiếu thông tin (mã chuyến, thời điểm), Vận hành phải hỏi lại khách. |
| **H2** | Hệ thống GPS ↔ Hệ thống chat / ghi âm | Dữ liệu nằm ở nhiều màn hình khác nhau, nhân viên phải tự khớp thời gian bằng tay. |
| **H3** | Vận hành → CSKH → Khách hàng & Tài xế | Kết quả đến chậm; khách thường đã rời bỏ dịch vụ trước khi nhận được phản hồi. |

> ⚠️ **Điểm yếu lớn nhất của quy trình hiện tại:** hệ thống chỉ xử lý **bị động** — sau khi khách đã hủy chuyến hoặc khiếu nại. Không có cơ chế phát hiện tài xế câu giờ **trong lúc** khách đang chờ.

---

## 3.2. Problem Statement (6-field) — Vin Smart Future Standard

| Field | Nội dung |
|---|---|
| **1. Actor / Operator** | **Chuyên viên Vận hành & CSKH (Operations/CSKH)** của Xanh SM — người xác minh và phê duyệt vụ việc. Bên liên quan trực tiếp: **khách hàng đặt xe** (phải chờ lâu, bị ép hủy) và **tài xế** (đối tượng bị xử lý). |
| **2. Current Workflow** | Khi khách khiếu nại hoặc tự hủy chuyến, nhân viên: **(1)** nhận ticket từ CSKH; **(2)** mở lịch sử cuốc xe và log GPS trên hệ thống nội bộ; **(3)** đọc chat in-app / nghe lại ghi âm cuộc gọi, đối chiếu với từng mốc GPS; **(4)** phân loại vi phạm theo quy định và ra quyết định xử phạt / hoàn phí. 4 bước, hoàn toàn thủ công, trên nhiều hệ thống rời rạc, mất **13-18 phút/lượt**. |
| **3. Bottleneck** | **Bước 3-4 (10-15 phút/lượt):** nhân viên phải nghe/đọc toàn bộ hội thoại rồi khớp thủ công với tọa độ GPS theo từng mốc thời gian. Việc phân loại dựa trên phán đoán chủ quan nên hai nhân viên có thể ra hai kết luận khác nhau cho cùng một vụ. Ngoài ra, **không có cảnh báo real-time** khi tài xế đứng yên hoặc đi sai hướng. |
| **4. Business Impact** | *(Số liệu giả định, cần xác minh với Khối Vận hành)* Khoảng **300 vụ cần xác minh/ngày** tại Hà Nội × 13-18 phút ≈ **65-90 giờ công/ngày** (tương đương 8-11 nhân sự toàn thời gian). Vụ việc tồn đọng khiến khách chờ phản hồi lâu, dễ rời bỏ dịch vụ; tài xế có thể lách quy định để né KPI tỷ lệ hủy; doanh thu cuốc xe bị thất thoát và uy tín thương hiệu bị ảnh hưởng. |
| **5. Success Metric** | **1. Efficiency:** Giảm thời gian xác minh một vụ từ **10-15 phút xuống dưới 1 phút**.<br>**2. Customer Experience:** Giảm **15%** tỷ lệ khách tự hủy do chờ lâu so với baseline trước triển khai.<br>**3. Quality:** Độ chính xác phân loại vi phạm đạt **≥ 90%**, đo trên tập vụ việc đã được nhân viên kiểm duyệt.<br>**4. Guardrail:** Tỷ lệ quyết định bị tài xế khiếu nại thành công **không tăng** so với baseline (không xử phạt oan). |
| **6. Operational Boundary** | **AI được phép:** đọc log GPS, trạng thái cuốc, chat in-app và bản phiên âm cuộc gọi của **đúng chuyến** bị gắn cờ; dựng timeline; phân loại dấu hiệu vi phạm; tạo hồ sơ nháp `[DRAFT_ONLY]` kèm trích dẫn và mức độ tin cậy.<br>**CẤM:** AI không được tự động trừ tiền, khóa tài khoản tài xế, từ chối khiếu nại hay phát hành quyết định cuối cùng; không kết luận khi thiếu bằng chứng trích dẫn; không đưa thông tin cá nhân (SĐT, địa chỉ) vào hồ sơ.<br>**Bắt buộc HITL:** mọi quyết định xử lý do nhân viên Vận hành/CSKH phê duyệt; tài xế luôn có quyền khiếu nại. |

---

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

---

# 🏁 Phase 5 — EVALUATE (Nhóm)

### AI Readiness Checklist:
1. [x] **Chúng tôi có sẵn dữ liệu mẫu/logs sạch để test?**
   Có một phần. Log GPS, trạng thái cuốc xe và chat in-app đã được hệ thống ghi lại đầy đủ. **Còn thiếu:** tập vụ việc đã gắn nhãn vi phạm để đo độ chính xác → cần gắn nhãn 300-500 vụ lịch sử trong 2 tuần đầu. Ghi âm cuộc gọi cần thêm bước chuyển giọng nói thành văn bản (STT) tiếng Việt.
2. [x] **Rủi ro khi AI sai có nằm trong tầm kiểm soát (qua HITL hoặc Fallback)?**
   Có. AI chỉ gắn cờ và tạo hồ sơ nháp; mọi quyết định xử lý tài xế đều do nhân viên duyệt. Khi LLM lỗi, không chắc chắn hoặc thiếu dữ liệu → tự động chuyển về quy trình thủ công. Rule cảnh báo sớm chỉ nhắc tài xế và cho khách đổi xe, không xử phạt ai.
3. [ ] **Stakeholders sẵn sàng thay đổi quy trình làm việc cũ?**
   Chưa hoàn toàn. Nhân viên Vận hành được lợi trực tiếp (giảm tải). Tuy nhiên **tài xế** có thể phản ứng với việc bị giám sát GPS và phân tích hội thoại → cần công bố chính sách minh bạch, cơ chế khiếu nại rõ ràng, và xác nhận phạm vi sử dụng dữ liệu với bộ phận Pháp chế trước khi triển khai.

### Quyết định cuối cùng của Ban Giám Đốc Vin Smart Future:
[x] **GO (Bắt đầu xây dựng Prototype):** Bắt đầu phát triển với scope hẹp.
[ ] **NOT YET (Cần tích lũy thêm dữ liệu/xác lập baseline):** Trì hoãn để chuẩn bị thêm.
[ ] **NO-GO (Không khả thi / Rule-based tốt hơn):** Hủy bỏ dự án AI này.

**Justification (Lý giải quyết định dựa trên bằng chứng kỹ thuật và chi phí):**
> * **Kỹ thuật khả thi:** Phần phát hiện qua GPS là Rule tất định, dễ kiểm thử. Phần LLM chỉ xử lý đoạn hội thoại ngắn của từng chuyến (phân loại + trích dẫn), nằm trong khả năng của các mô hình hiện nay như Gemini 2.5 Flash.
> * **Chi phí hợp lý:** LLM chỉ được gọi cho các chuyến **bị gắn cờ hoặc có khiếu nại**, không phải mọi chuyến → chi phí mỗi vụ rất nhỏ so với 10-15 phút công của một nhân viên.
> * **Rủi ro kiểm soát được:** HITL bắt buộc ở bước ra quyết định, Fallback rõ ràng cho mọi trường hợp lỗi — sai sót của AI không trực tiếp gây thiệt hại cho tài xế hay khách.
> * **Vì sao không chọn NOT YET:** Hai điểm còn thiếu (dữ liệu gắn nhãn, sự đồng thuận của tài xế) có thể giải quyết **ngay trong giai đoạn pilot** qua shadow mode và truyền thông chính sách, không cần trì hoãn toàn bộ dự án.
> * **Vì sao không phải NO-GO:** Rule đơn thuần giải quyết được phần GPS nhưng **không hiểu được hội thoại** — không phát hiện được các câu ép khách tự hủy, vốn là bằng chứng quan trọng nhất trong Bước 3-4.

### Kế hoạch Pilot (scope hẹp):

| Giai đoạn | Thời gian | Nội dung | Điều kiện qua giai đoạn |
|---|---|---|---|
| **1. Baseline** | Tuần 1-2 | Đo thời gian xác minh và tỷ lệ khách tự hủy do chờ lâu hiện tại; gắn nhãn 300-500 vụ lịch sử | Có baseline và tập test |
| **2. Shadow mode** | Tuần 3-4 | AI tạo hồ sơ nháp song song, nhân viên vẫn làm thủ công; so sánh kết quả | Độ khớp với nhân viên ≥ 90% |
| **3. Pilot thật** | Tuần 5-8 | 1 khu vực tại Hà Nội, chỉ dùng GPS + chat in-app (chưa dùng ghi âm); bật cảnh báo sớm cho một nhóm chuyến để so sánh A/B | Xác minh < 1 phút; tỷ lệ tự hủy giảm; không tăng khiếu nại xử phạt oan |

**Điều kiện dừng:** Độ chính xác < 80% sau khi đã tinh chỉnh prompt, hoặc số khiếu nại xử phạt oan của tài xế tăng so với baseline.
