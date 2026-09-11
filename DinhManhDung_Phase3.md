# 🏗️ Phase 3 — DEEP-DIVE
**Bài toán:** Hệ thống không tự động phát hiện được tài xế câu giờ, không tuân thủ điểm đón ép khách tự hủy chuyến (Xanh SM).

## 3.1. Current-State Workflow
Quy trình xử lý khiếu nại tài xế câu giờ / ép khách hủy chuyến hiện tại của nhân viên CSKH Xanh SM:

```text
┌──────────────┐     ┌──────────────┐     ┌──────────────┐     ┌──────────────┐
│ Bước 1       │     │ Bước 2       │     │ Bước 3       │     │ Bước 4       │
│ Hệ thống nhận│     │ Tra cứu định │     │ Nghe ghi âm &│     │ Đối chiếu &  │
│ khiếu nại/hủy│ ──→ │ vị GPS của xe│ ──→ │ đọc chat KH  │ ──→ │ ra QĐ phạt   │
│ chuyến từ App│     │ trên hệ thống│     │ và Tài xế    │     │ Tài xế       │
│ Ai: Hệ thống │     │ Ai: CSKH     │     │ Ai: CSKH     │     │ Ai: CSKH     │
│ ⏱ 1 phút    │     │ ⏱ 2 phút     │     │ ⏱ 7 phút    │     │ ⏱ 5 phút     │
│ In: App Xanh │     │ In: Ticket ID│     │ In: Logs/Call│     │ In: Bằng chứng
│ Out: Ticket  │     │ Out: Lộ trình│     │ Out: Tình tiết│     │ Out: QĐ phạt │
└──────────────┘     └──────────────┘     └──────────────┘     └──────────────┘

🔄 = Handoff (Chuyển giao từ Hệ thống sang CSKH)
🔴 = Bottlenecks
⏱ Tổng thời gian xử lý thủ công: 15 phút/lượt.
```
