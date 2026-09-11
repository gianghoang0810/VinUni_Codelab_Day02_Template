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