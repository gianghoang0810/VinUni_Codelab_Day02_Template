# Lab 02 — Worksheet: AI Product Scoping (Vin Smart Future)

---

## 🏛️ 1. Bối cảnh thực tế: Vin Smart Future (Vingroup)

**Vingroup** — Tập đoàn tư nhân lớn nhất Việt Nam — vừa sáp nhập toàn bộ các phòng ban công nghệ thuộc các công ty thành viên thành một đơn vị công nghệ thống nhất mang tên **Vin Smart Future**. 

Nhiệm vụ của **Vin Smart Future** là xây dựng các giải pháp AI, số hóa, và tự động hóa cốt lõi để nâng cao hiệu suất vận hành và trải nghiệm khách hàng xuyên suốt các công ty thành viên:
* 🚗 **VinFast:** Hệ thống xe điện thông minh (EV), trợ lý AI ảo trong xe, dự đoán bảo trì pin, và quản lý chuỗi cung ứng sản xuất.
* 🚕 **Xanh SM (GSM):** Vận hành đội xe taxi/xe máy điện thông minh, điều vận thông minh (Smart Dispatching), tối ưu hóa lộ trình di chuyển.
* 🏢 **Vinhomes:** Quản lý đô thị thông minh (Smart Cities), trợ lý cư dân thông minh, tối ưu hóa mức tiêu thụ năng lượng.
* 🏥 **Vinmec:** Y tế thông minh, chẩn đoán hình ảnh bằng AI, tối ưu hóa quản lý hồ sơ bệnh án.
* 🎢 **Vinpearl / VinWonders:** Trải nghiệm du lịch số hóa, quản lý phòng và luồng khách thông minh tại các khu vui chơi.

Trong buổi Lab hôm nay, nhóm của bạn sẽ đóng vai trò là **AI Product Engineer** tại **Vin Smart Future**, tiến hành tìm kiếm, scoping, phân tích độ khả thi, thiết lập ranh giới vận hành, và xây dựng một **bản mẫu kỹ thuật (prompt prototype)** cho một bài toán cụ thể thuộc một trong những mảng kinh doanh trên.

---

## 📊 2. Cơ cấu tính điểm bài lab

### 👥 Điểm nhóm (60 điểm)

| Gate | Điểm | Deliverable | Tiêu chí chấm |
|---|---:|---|---|
| **G1. Workflow Mapping** | 20 | Problem Deep-Dive | Vẽ chi tiết quy trình hiện tại: các bước, handoff, thời gian, bottleneck |
| **G2. Problem Statement** | 20 | Problem Deep-Dive | Problem Statement 6-field bám sát thực tế, metric có số và ranh giới rõ ràng |
| **G3. AI Fit & Future Flow** | 10 | Problem Deep-Dive | So sánh Rule vs LLM vs Agent, future flow có bước AI, ranh giới và Fallback |
| **G4. Decision Quality** | 10 | Problem Deep-Dive | Quyết định Go/Not Yet/No-Go trung thực và có chứng cứ rõ ràng |

### 👤 Điểm cá nhân (40 điểm)

| Gate | Điểm | Deliverable | Tiêu chí chấm |
|---|---:|---|---|
| **I1. Scan & Cards** | 15 | Quick Cards | Liệt kê 5 problems sử dụng 3 lenses, hoàn thiện 3 quick cards chất lượng |
| **I2. Prototyping** | 10 | 02-lab/ | Chạy thử nghiệm programmatic prompt prototype thành công |
| **I3. AI Log & Reflection** | 15 | 03-ai-log.md | Phản ánh trung thực về việc dùng AI làm thought-partner (giúp gì, sai gì, sửa gì) |

---

# 🚀 Phase 0 — worked Example: Xanh SM Intelligent Dispatcher (15 min)

*Giảng viên walk-through ví dụ thực tế từ Vin Smart Future để bạn hiểu rõ cách scoping một bài toán AI.*
Đọc chi tiết worked example tại file [02-deliverable-example.md](02-deliverable-example.md).

---

# 🔍 Phase 1 — SCAN (Cá nhân, 20 min)

Hãy sử dụng **4 Lenses** dưới đây để quét qua hoạt động vận hành của các công ty thành viên Vingroup. Ghi lại **ít nhất 5 bài toán/bottleneck** thực tế.

### 4 Lenses tìm bài toán AI cho Vingroup:
1. **Lặp lại (Repetitive):** Tác vụ lặp đi lặp lại nhiều lần hằng ngày. (Ví dụ: So khớp hóa đơn sạc điện tại VinFast, route lại chuyến taxi tại Xanh SM).
2. **Tốn thời gian (Time-consuming):** Tác vụ ngốn thời gian xử lý thủ công của nhân viên. (Ví dụ: Soạn thảo phản hồi đánh giá 1-star của cư dân Vinhomes).
3. **AI có thể tốt hơn (AI-upgrade):** Dịch vụ khách hàng hiện tại còn chậm hoặc phản hồi rập khuôn. (Ví dụ: Chatbot CSKH Vinpearl hỗ trợ đặt vé vui chơi).
4. **Pain từ người khác (Stakeholder Pain):** Bottleneck khiến khách hàng hoặc nhân viên thực địa phàn nàn. (Ví dụ: Tài xế Xanh SM phàn nàn về việc hệ thống gợi ý điểm đón khách không chính xác).

> [!TIP]
> **🤖 AI Prompts — Partner brainstorm:**
> Hãy sử dụng prompt sau để brainstorm các bài toán thực tế nếu bạn chưa có ý tưởng:
> *"Tôi là AI Engineer tại Vin Smart Future (Vingroup). Tôi đang tìm kiếm các pain point vận hành cụ thể có thể tối ưu bằng AI cho mảng [Chọn một: VinFast / Xanh SM / Vinhomes / Vinmec]. Hãy gợi ý cho tôi 5 quy trình nghiệp vụ thủ công, tốn nhiều thời gian và gây rò rỉ hiệu suất kèm con số thống kê ước tính về tổn thất."*

### 📝 List bài toán của tôi:
| # | Subsidiary (VinFast/Xanh SM...) | Lens | Mô tả ngắn bài toán |
|---|----------------------------------|------|---------------------|
| 1 | | | |
| 2 | | | |
| 3 | | | |
| 4 | | | |
| 5 | | | |

---

# 🃏 Phase 2 — QUICK-ASSESS (Cá nhân, 30 min)

Chọn **top 3 bài toán** từ danh sách trên và hoàn thiện **3 Quick Problem Cards** dưới đây (10 phút/card).

```
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #___                                     │
│                                                             │
│ Bài toán (1 câu): ________________________________________  │
│ Công ty thành viên: [ ] VinFast  [ ] Xanh SM  [ ] Vinhomes  │
│                     [ ] Vinmec   [ ] Khác (Ghi rõ)________  │
│                                                             │
│ Ai đang đau (Actor)? ______________________________________ │
│                                                             │
│ Workflow thủ công hiện tại (3-5 bước):                      │
│   1. ___ ──> 2. ___ ──> 3. ___ ──> 4. ___                   │
│                                                             │
│ Bước nào tốn thời gian/lỗi nhất? ___ (⏱ ___ phút/lượt)      │
│ AI có thể nhảy vào hỗ trợ ở bước nào? _____________________ │
│                                                             │
│ Đo thành công bằng gì (Metric có số)? ______________________ │
│   VD: "Giảm thời gian soạn phản hồi từ 10 min ──> under 2 min"│
│                                                             │
│ Quick Architecture: [ ] No AI  [ ] Rule  [ ] LLM  [ ] Agent │
└─────────────────────────────────────────────────────────────┘
```

> [!TIP]
> **🤖 AI Prompts — Stress-Test thẻ bài toán:**
> Hãy dán nội dung thẻ bài toán của bạn vào LLM để nhận phản biện:
> *"Đây là một thẻ bài toán vận hành tôi đề xuất cho Vin Smart Future: [Dán nội dung]. Hãy đóng vai trò là một CFO và Trưởng phòng Vận hành cực kỳ khắt khe, chỉ ra cho tôi 3 điểm yếu về logic, metric, và giải thích vì sao rule-based code thông thường có thể giải quyết bài toán này tốt hơn là dùng AI."*

---

# 🏗️ Phase 3 — DEEP-DIVE (Nhóm, 85 min)

## 3.1. Current-State Workflow Mapping (25 min)
**Vẽ quy trình hiện tại lên bảng/giấy A3.** Sử dụng các ký hiệu:
* 🔴 **Bottleneck:** Bước gây tắc nghẽn, tốn thời gian, hoặc sai sót nhiều nhất.
* 🔄 **Handoff:** Điểm chuyển giao thông tin giữa người và hệ thống, hoặc giữa các bộ phận.
* Ghi rõ thời gian vận hành trung bình: **Tổng cộng = ____ phút/lượt**.

## 3.2. Problem Statement (6-field) & Metrics (15 min)
Điền đầy đủ 6 trường thông tin của bài toán:

| Field | Nội dung chi tiết |
|---|---|
| **1. Actor / Operator** | Ai đang thực hiện tác vụ hằng ngày? |
| **2. Current Workflow** | Mô tả tóm tắt quy trình thủ công hiện tại và công cụ sử dụng. |
| **3. Bottleneck** | Bước nào chậm, lỗi, hoặc cần xử lý ngôn ngữ tự động nhiều nhất? |
| **4. Business Impact** | Tổn thất thực tế đo bằng thời gian, chi phí, hoặc SLA của Vingroup. |
| **5. Success Metric** | AI giải quyết được thì đạt ngưỡng số mấy? (Ví dụ: *"85% vé được phân loại dưới 10s"*). |
| **6. Operational Boundary** | AI được phép làm gì, TUYỆT ĐỐI không được làm gì, điểm nào cần duyệt? |

## 3.3. Future-State Flow & AI Fit (25 min)

### 1. Xác định mức AI Fit (AI-Fit Matrix)
* **Lựa chọn kiến trúc:** `[ ] Rule / State-Machine` &nbsp;&nbsp;&nbsp;&nbsp; `[x] LLM Feature (kết hợp Rule Filter)` &nbsp;&nbsp;&nbsp;&nbsp; `[ ] Agentic Loop`
* **Lý giải quyết định (AI-Fit Rationale):**
  * **Vì sao không chọn thuần Rule-based?** Dữ liệu GPS/tốc độ (ví dụ: xe đứng yên > 5 phút) chỉ phản ánh hiện tượng nhưng không hiểu được ngữ cảnh (do kẹt xe thực tế, ngập nước hay cố tình câu giờ). Rule-based không thể phân tích ngữ nghĩa tinh vi trong tin nhắn hoặc cuộc gọi của tài xế (như dùng từ ngữ gợi ý "khách tự hủy giúp em", báo hỏng xe giả mạo, viện cớ lòng vòng để ép khách bỏ cuộc).
  * **Vì sao chọn LLM Feature?** LLM cực kỳ mạnh trong việc hiểu ngữ cảnh giao tiếp (Intent Recognition), phát hiện dấu hiệu thao túng tâm lý / ép hủy chuyến, trích xuất chính xác câu nói làm bằng chứng (Evidence Extraction) kèm mốc thời gian, đồng thời đối chiếu với dữ liệu hành trình GPS để gắn nhãn mức độ vi phạm theo Quy tắc ứng xử của Xanh SM.
  * **Vì sao không chọn Full Agentic Loop tự động hóa 100%?** Việc ban hành chế tài xử phạt (trừ điểm tín nhiệm, phạt tiền, khóa app tài xế) hoặc hoàn tiền/bồi thường cho khách hàng là các hành động có tác động trực tiếp đến thu nhập của tài xế và chi phí công ty, tiềm ẩn rủi ro pháp lý nếu AI kết luận sai (False Positive). Do đó, cần cơ chế **Human-in-the-loop (HITL)** — AI làm trợ lý phân tích và đề xuất quyết định trong 5 giây, con người phê duyệt cuối cùng trong 30 giây.

---

### 2. Sơ đồ quy trình tương lai (Future-State Flow)

```text
┌───────────────────────────┐      ┌───────────────────────────┐      ┌───────────────────────────┐
│ BƯỚC 1: SỰ KIỆN KÍCH HOẠT  │      │ BƯỚC 2: TIỀN XỬ LÝ DỮ LIỆU │      │ BƯỚC 3: AI PHÂN TÍCH &    │
│                           │      │                           │      │        TRÍCH XUẤT CHỨNG CỨ│
│ Khách hủy chuyến / Phàn nàn│ ───> │ 🔵 Auto-Ingest Dữ liệu:   │ ───> │ 🔵 LLM Vi phạm Detector:  │
│ hoặc Rule GPS phát hiện   │      │ • Audio cuộc gọi ──> STT  │      │ • Phân tích hội thoại     │
│ xe đứng yên/đi chệch >7p  │      │ • Toàn bộ Chat logs       │      │ • Phát hiện hành vi ép hủy│
│                           │      │ • Telemetry GPS hành trình│      │ • Trích xuất bằng chứng   │
│ Hệ thống tự động          │      │ Microservice Data Pipeline│      │ ⏱ Xử lý: ~3 - 5 giây      │
└───────────────────────────┘      └───────────────────────────┘      └───────────────────────────┘
                                                                                    │
                                                                                    ▼
┌───────────────────────────┐      ┌───────────────────────────┐      ┌───────────────────────────┐
│ BƯỚC 5: TỰ ĐỘNG THỰC THI  │      │ BƯỚC 4: DUYỆT QUYẾT ĐỊNH  │      │ BẢNG ĐỀ XUẤT CỦA AI       │
│                           │      │        (HUMAN-IN-THE-LOOP)│      │                           │
│ Gửi thông báo chế tài tài │ <─── │ 🟢 Nhân viên Vận hành/CSKH│ <─── │ • Tỷ lệ vi phạm: 95%      │
│ xế + Hoàn tiền / Voucher  │      │ xem 1 trang tóm tắt &     │      │ • Bằng chứng: Quote + GPS │
│ xin lỗi gửi vào App khách │      │ click "Duyệt chế tài"     │      │ • Đề xuất: Phạt mức 2     │
│ ⏱ Tự động trong 1 giây    │      │ ⏱ Ra quyết định: < 30 giây│      │                           │
└───────────────────────────┘      └───────────────────────────┘      └───────────────────────────┘
                                                  │
                                                  ▼
                                       ┌───────────────────────────┐
                                       │ ↩️ FALLBACK MECHANISM     │
                                       │                           │
                                       │ 1. Độ tin cậy AI < 80%    │
                                       │    hoặc file âm thanh lỗi │
                                       │    ──> Chuyển hàng đợi    │
                                       │    thẩm định thủ công.    │
                                       │ 2. Nhân viên phát hiện    │
                                       │    AI bắt nhầm (kẹt xe)   │
                                       │    ──> Bấm "Reject & Log" │
                                       │    lưu dữ liệu huấn luyện.│
                                       └───────────────────────────┘
```

#### Chi tiết các bước trong Future-State Flow:
* 🔵 **AI Steps (Tác vụ AI xử lý tự động):**
  1. **Audio STT & Log Aggregation:** Tự động chuyển băng ghi âm cuộc gọi tổng đài / in-app call thành văn bản, gom cùng tin nhắn chat nội bộ và tọa độ GPS của cuốc xe.
  2. **LLM Violation Detection & Evidence Summarization:** LLM phân tích ngữ cảnh hội thoại, so khớp với diễn biến GPS (xe đứng yên hay di chuyển ngược hướng điểm đón). Trả về JSON cấu trúc gồm: `violation_detected` (true/false), `violation_type` ("coaching_customer_to_cancel", "delaying_pickup", "none"), `confidence_score` (0.0 - 1.0), `evidence_quote` (câu nói cụ thể của tài xế), và `recommended_penalty` (theo SOP Xanh SM).
* 🟢 **Human Step (HITL - Phê duyệt có con người kiểm soát):**
  * Nhân viên vận hành/CSKH không cần nghe lại 15 phút băng ghi âm hay đối soát thủ công từng tọa độ. Dashboard hiển thị thẻ sự cố đã được AI phân tích sẵn kèm bằng chứng nổi bật.
  * Nhân viên chỉ mất **20–30 giây** để đọc lướt qua bằng chứng, bấm nút **"Xác nhận xử phạt"** hoặc **"Bác bỏ"**.
* ↩️ **Fallback Plan (Kế hoạch dự phòng khi AI lỗi hoặc không tự tin):**
  * **Fallback 1 (Chất lượng dữ liệu kém / Model Low-Confidence):** Nếu âm thanh bị rè, STT không dịch được hoặc LLM trả về điểm tin cậy `confidence_score < 0.80`, hệ thống tự động gắn cờ `[FLAG_MANUAL_REVIEW]` và đẩy về quy trình nghe/đọc thủ công truyền thống.
  * **Fallback 2 (Overruling & Model Drift):** Nếu nhân viên nhận thấy AI phán đoán sai (ví dụ: tài xế giải thích hợp lý do sự cố bất khả kháng trên đường được xác thực), nhân viên bấm ghi đè phán quyết, hệ thống tự động lưu case này vào dataset để tinh chỉnh lại Prompt/Few-shot.

---

# 💻 Phase 4 — TECHNICAL PROMPT PROTOTYPE (Nhóm, 30 min)

Để đảm bảo kỹ sư của Vin Smart Future luôn giữ vững năng lực lập trình, nhóm của bạn sẽ tiến hành **lập trình bản mẫu prompt** trực tiếp trên **Gemini 2.5 Flash** bằng Python để stress-test hệ thống.

### Hướng dẫn thực hiện:
1. Mở file [starter-code/prompt_prototype.py](starter-code/prompt_prototype.py) bằng VS Code/Cursor.
2. Hoàn thiện các nội dung sau:
   * **System Prompt:** Viết chỉ thị cực kỳ nghiêm ngặt quy định vai trò, nhiệm vụ, định dạng output và **Operational Boundary (Ranh giới cấm)** của mô hình.
   * **Structured Output:** Định nghĩa định dạng JSON output rõ ràng.
   * **Adversarial Test Cases:** Viết ít nhất 3 prompts "tấn công" (Adversarial inputs) cố tình dụ AI vượt ranh giới hoặc đưa ra câu trả lời không được phép để kiểm tra xem ranh giới của bạn có thực sự vững chắc.
3. Chạy file python:
   ```bash
   python3 prompt_prototype.py
   ```
4. Kiểm tra xem các ranh giới an toàn có bị LLM phá vỡ hay không và ghi lại kết quả vào worksheet.

---

# 🏁 Phase 5 — EVALUATE (Nhóm, 20 min)

### AI Readiness Checklist:
1. [ ] Chúng tôi có sẵn dữ liệu mẫu/logs sạch để test?
2. [ ] Rủi ro khi AI sai có nằm trong tầm kiểm soát (qua HITL hoặc Fallback)?
3. [ ] Stakeholders sẵn sàng thay đổi quy trình làm việc cũ?

### Quyết định cuối cùng của Ban Giám Đốc Vin Smart Future:
[ ] **GO (Bắt đầu xây dựng Prototype):** Bắt đầu phát triển với scope hẹp.
[ ] **NOT YET (Cần tích lũy thêm dữ liệu/xác lập baseline):** Trì hoãn để chuẩn bị thêm.
[ ] **NO-GO (Không khả thi / Rule-based tốt hơn):** Hủy bỏ dự án AI này.

**Justification (Lý giải quyết định dựa trên bằng chứng kỹ thuật và chi phí):**
> *Viết lý giải chi tiết tại đây*

---

# 📝 Phase 6 — REFLECTION (Cá nhân)
*Ghi nhận phản ánh của cá nhân bạn về việc phối hợp với AI trong buổi học hôm nay vào file `03-ai-log.md`.*
