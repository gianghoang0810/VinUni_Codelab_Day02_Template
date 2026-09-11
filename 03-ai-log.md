# 03 — AI Log & Reflection (Nguyễn Văn Quốc Việt)

> **Nhật ký tương tác AI — Lab 02: AI Product Scoping (Phase 6 — REFLECTION, Cá nhân).**
>
> * **Công cụ AI sử dụng:** **Claude** (qua Claude Code, tích hợp trong VS Code).
> * **Vai trò của AI:** Thought-partner khi scoping bài toán, trợ lý định dạng tài liệu theo bài mẫu, và trợ lý kỹ thuật (Git, Python, Gemini SDK).
> * **Nguyên tắc tôi đặt ra:** Ý tưởng bài toán và quyết định cuối cùng là của tôi và nhóm; AI hỗ trợ trình bày, phản biện và thực thi. Mọi số liệu AI đưa ra phải được kiểm tra lại.

---

## 1. Tôi đã dùng AI vào những việc gì?

| Phase | Tôi yêu cầu | AI đã làm | Phần do tôi / nhóm quyết định |
|---|---|---|---|
| **Phase 1 — SCAN** | Trình bày 5 bài toán của tôi theo style của bài mẫu `02-deliverable-example.md` | Định dạng lại bảng, sửa lỗi chính tả ("Paint" → "Pain", "VinHomes" → "Vinhomes") | 5 bài toán và Lens của từng bài do tôi tự tìm |
| **Phase 2 — QUICK-ASSESS** | Làm Quick Card cho bài #1, #2, #4 | Soạn workflow, bottleneck, metric cho 3 card; căn khung card bằng script | Chọn bài nào để làm card; card Xanh SM (#3) do tôi tự viết |
| **Phase 3 — DEEP-DIVE** | Làm phần 3.3 Future-State & AI Fit cho card Xanh SM; bổ sung 3.1, 3.2 | So sánh Rule / LLM / Agent, vẽ future flow có Fallback và HITL; đọc file của các bạn trong nhóm để đồng bộ 3.1, 3.2 | Bài toán Xanh SM là lựa chọn chung của nhóm |
| **Phase 5 — EVALUATE** | Bổ sung phần còn thiếu | Đề xuất checklist, quyết định GO kèm kế hoạch pilot | Quyết định GO / NOT YET cần nhóm thống nhất |
| **Phase 4 — PROTOTYPE** | Làm file `prompt_prototype.py` | Viết `SYSTEM_PROMPT`, hàm gọi Gemini, thêm test tấn công thứ 3, cài môi trường, chạy thử autograder | Tự lấy API key và chạy kiểm thử thật |
| **Git / GitHub** | Tạo branch, commit, push, sửa lỗi | Hướng dẫn lệnh, xử lý lỗi `index.lock`, kiểm tra xem tôi đã push lên đâu | Tự chạy lệnh commit / push trên branch cá nhân |

---

## 2. AI đã giúp tôi những gì?

* **Tiết kiệm thời gian trình bày:** AI chuyển nội dung thô của tôi thành bảng và Quick Card đúng format bài mẫu, căn khung ASCII thẳng hàng (việc làm tay rất mất thời gian vì tiếng Việt có dấu).
* **Phản biện kiến trúc AI:** Card Xanh SM của tôi ban đầu chọn **LLM**. Khi làm 3.3, AI chỉ ra rằng phần phát hiện "xe đứng yên / đi sai hướng" là tín hiệu GPS nên dùng **Rule** sẽ nhanh, rẻ và chính xác hơn; LLM chỉ nên dùng cho phần hiểu hội thoại. Tôi đồng ý và chuyển sang **Rule + LLM (Hybrid)**.
* **Tương tự, với Card #4 (Vinhomes HVAC):** AI thẳng thắn đánh giá bài này **không cần LLM** (cảm biến + Rule + ML dự báo), đúng tinh thần *"Problem First, AI Second"* của Inspiration Kit.
* **Phát hiện các ràng buộc ẩn trong đề:**
  * Autograder chỉ tìm đúng 4 tên file `01-problem-scan.md`, `02-deep-dive-report.md`, `03-ai-log.md`, `04-workflow-diagram.*` → các file tên tùy ý (như `VIET.md`) sẽ không được tính điểm.
  * Autograder chấm `SYSTEM_PROMPT` theo từ khóa cố định (`draft_only`, `5%`, `dispatch_mobile_charger`) → phải giữ đúng tình huống Xanh SM hết pin trong prototype.
  * Autograder giới hạn 30 giây cho cả script → AI tắt chế độ "thinking" của Gemini 2.5 Flash để phản hồi nhanh hơn.
  * Script có thể bị crash khi in emoji / tiếng Việt trên Windows lúc autograder chạy → AI thêm cấu hình UTF-8.
* **Gỡ rối Git:** AI chẩn đoán lỗi *"Another git process"* là do file `.git/index.lock` còn sót lại sau một lệnh bị ngắt, kiểm tra không có tiến trình git nào đang chạy rồi mới xóa.

---

## 3. AI đã sai, "bịa" hoặc hiểu sai ở đâu?

| # | Vấn đề | Ví dụ cụ thể | Rủi ro | Cách tôi xử lý |
|---|---|---|---|---|
| 1 | **Tự đặt số liệu không có nguồn** | "~300 vụ cần xác minh/ngày", tỉ lệ chatbot tự xử lý "30% → 70%", học lý thuyết "16 giờ → 6 giờ", các ngưỡng "đứng yên > 3 phút", "confidence < 0.7" | Người đọc tưởng là số liệu thật của Vingroup → sai lệch khi ra quyết định | Yêu cầu ghi rõ **"số liệu giả định, cần xác minh"** trong báo cáo; coi đây là giả thuyết cần kiểm chứng ở giai đoạn baseline |
| 2 | **Thêm chi tiết tôi không yêu cầu** | Tự thêm ví dụ "(gia đình, cặp đôi, đoàn)" vào mô tả bài #1 | Nội dung không còn hoàn toàn là của tôi | Kiểm tra lại từng thay đổi so với bản gốc tôi đưa |
| 3 | **Hiểu sai câu hỏi mơ hồ** | Tôi hỏi *"Cách để code"* (ý là lệnh để đưa phần 3.3 lên branch), AI lại hiểu thành cách làm bài code Python | Mất thời gian, trả lời lạc đề | Ngắt ngang và nói rõ: *"Ý tôi là bạn hãy chỉ tôi cách up lên branch của tôi phần 3.3"* |
| 4 | **Số thứ tự card bị trùng** | Card Xanh SM tôi đánh là #2, trùng với Card #2 Vinpearl mà AI đã làm | Người chấm nhầm lẫn giữa các card | Đánh số lại theo số thứ tự trong bảng SCAN (Card #3), giống cách bài mẫu làm |
| 5 | **Số liệu giữa các phần không khớp** | Card ghi Bước 3-4 mất 10-15 phút, nhưng bản 3.1 của nhóm ghi tổng cả quy trình chỉ 12-15 phút | Báo cáo mâu thuẫn, mất điểm G1 / G2 | AI điều chỉnh tổng thành 13-18 phút cho khớp; **tôi cần thống nhất lại với nhóm** |
| 6 | **AI tự đề xuất quyết định thay nhóm** | AI chọn **GO** trong Phase 5 và tự viết lý do loại các card khác | Quyết định không phản ánh ý kiến của nhóm | Coi đây là **đề xuất**, mang ra họp nhóm trước khi merge vào `main` |

---

## 4. Tôi đã sửa prompt và đặt ranh giới như thế nào?

| Prompt ban đầu (chưa tốt) | Vấn đề | Prompt đã sửa (tốt hơn) |
|---|---|---|
| *"Xóa request đó đi"* | Không rõ "request" là gì — thực tế repo không có pull request nào | AI hỏi lại và đưa ra các lựa chọn; tôi chọn rõ: **xóa branch ở cả GitHub và trên máy** |
| *"Cách để code"* | Quá ngắn, không nói rõ mục tiêu | *"Hãy chỉ tôi cách up lên branch của tôi phần 3.3"* |
| *"Tạo branch mới để up Phase 1"* | Thiếu thông tin danh tính commit | Bổ sung: *"với gmail là nguyenvanquocviet011@gmail.com"* |
| — | — | Prompt hiệu quả nhất: đưa **dữ liệu của tôi + file mẫu cụ thể + phần cần làm**, ví dụ: dán nguyên Quick Card rồi yêu cầu *"làm tương tự như phần 3.3 Future-State Flow & AI Fit"* |

**Bài học:** Prompt càng có **ngữ cảnh cụ thể** (dữ liệu gốc, file mẫu, phạm vi) thì AI càng ít phải đoán, ít sai.

---

## 5. Ranh giới tôi tự đặt khi làm việc với AI

* 🔑 **Không đưa API key vào chat hoặc vào code** — chỉ khai báo qua biến môi trường `GEMINI_API_KEY` trên máy.
* 🌿 **Chỉ push lên branch cá nhân**, không push lên `main` — việc merge vào `main` là của trưởng nhóm sau khi cả nhóm review.
* ✋ **Thao tác khó hoàn tác phải hỏi trước:** khi tôi yêu cầu xóa, AI kiểm tra và hỏi lại xóa cái gì trước khi thực hiện.
* 🧪 **Không tin kết quả khi chưa kiểm chứng:** số liệu phải gắn nhãn giả định; prototype phải chạy thật với Gemini mới biết ranh giới có vững không.
* 🧠 **Quyết định là của con người:** chọn bài toán, chọn kiến trúc và quyết định GO / NO-GO do tôi và nhóm chốt.

---

## 6. Kết quả Prototype (Phase 4)

| Tiêu chí autograder | Kết quả |
|---|---|
| `SYSTEM_PROMPT` có chỉ thị ranh giới | ✅ PASS (đủ `draft_only`, `5%`, `dispatch_mobile_charger`) |
| `evaluate_prompt()` dùng Gemini SDK | ✅ PASS |
| Có ≥ 2 Adversarial test hợp lệ | ✅ PASS (3 test: pin 2% đòi đi trạm 8km; bắt bỏ thẻ `[DRAFT_ONLY]`; giả danh Trưởng ca ra lệnh bỏ quy tắc) |
| Script chạy thành công với Gemini thật | ⏳ Chờ chạy với API key |
| Vượt qua toàn bộ kiểm tra ranh giới | ⏳ Chờ chạy với API key |

---

## 7. Bài học rút ra

1. **AI mạnh nhất ở trình bày và phát hiện ràng buộc**, nhưng **yếu ở số liệu thực tế** — nó sẽ đưa ra con số "nghe hợp lý" dù không có nguồn. Người dùng phải tự gắn nhãn và kiểm chứng.
2. **AI không chỉ làm theo mà còn phản biện được** (LLM → Rule + LLM, Card #4 không cần LLM) — nhưng tôi phải hiểu lý do thì mới bảo vệ được lựa chọn khi thuyết trình.
3. **Câu lệnh mơ hồ dẫn đến kết quả sai** — cần nói rõ mục tiêu, phạm vi và file tham chiếu.
4. **Làm việc nhóm cần đồng bộ:** AI giúp đối chiếu với file của các bạn, nhưng việc thống nhất số liệu và quyết định cuối cùng phải qua thảo luận nhóm.
