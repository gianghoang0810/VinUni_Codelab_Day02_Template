# 🔍 Phase 1 — SCAN (Cá nhân, 20 min)

📝 **List bài toán của tôi:**

| # | Subsidiary (VinFast/Xanh SM...) | Lens | Mô tả ngắn bài toán |
| :--- | :--- | :--- | :--- |
| 1 | VinFast | AI có thể tốt hơn | Trải nghiệm người dùng với trợ lý ảo (Vivi) đôi khi còn cứng nhắc, chưa hiểu được ngữ cảnh phức tạp hoặc thói quen cá nhân của tài xế. |
| 2 | Vinmec | Tốn thời gian | Bác sĩ tốn quá nhiều thời gian gõ văn bản/nhập liệu hồ sơ bệnh án (EMR) sau mỗi lượt khám thay vì dành thời gian tư vấn. |
| 3 | Vinpearl | Lặp lại | Khó khăn trong việc xếp lịch ca làm cho hàng ngàn nhân viên buồng phòng/phục vụ linh hoạt theo lượng khách booking biến động mỗi ngày. |
| 4 | Xanh SM (GSM) | Stakeholder Pain | Khách hàng phải chờ xe lâu vào giờ cao điểm do xe phân bổ không đều; tài xế tốn thời gian "chạy rỗng" tìm trạm sạc. |
| 5 | Vinhomes | AI có thể tốt hơn | Lãng phí năng lượng điện/HVAC tại các khu vực tiện ích chung (Sảnh, NSHCĐ, Hành lang) do bật/tắt theo lịch cứng thay vì theo lưu lượng người thực tế. |

---

# 🎴 Phase 2 — QUICK-ASSESS (Cá nhân, 30 min)

Chọn **top 3 bài toán** từ danh sách trên và hoàn thiện **3 Quick Problem Cards** dưới đây (10 phút/card).

```text
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #1                                       │
│                                                             │
│ Bài toán: Lãng phí năng lượng điện/HVAC tại các khu vực     │
│ tiện ích chung (Sảnh, NSHCĐ, Hành lang) do bật/tắt theo lịch│
│ cứng thay vì theo lưu lượng người thực tế.                  │
│                                                             │
│ Công ty thành viên: [ ] VinFast  [ ] Xanh SM  [x] Vinhomes  │
│                     [ ] Vinmec   [ ] Khác (Ghi rõ)________  │
│                                                             │
│ Ai đang đau (Actor)?                                        │
│ - Ban Quản lý (thâm hụt chi phí vận hành, áp lực Net Zero). │
│ - Cư dân (bức xúc vì bị khóa phòng NSHCĐ/hạn chế máy lạnh). │
│ - Kỹ thuật/Bảo vệ (mất thời gian đi tuần tra bật/tắt thủ    │
│   công từng tầng).                                          │
│                                                             │
│ Workflow thủ công hiện tại (4 bước):                        │
│   1. BQL chốt lịch vận hành cố định theo khung giờ định sẵn │
│   → 2. Bảo vệ/kỹ thuật đi bộ đến tận nơi bật CB, máy lạnh   │
│   → 3. Thiết bị chạy 100% công suất dù vắng hoặc không người│
│   → 4. Hết giờ, nhân viên đến tắt (hoặc quên tắt qua đêm)   │
│                                                             │
│ Bước nào tốn thời gian/lỗi nhất?                             │
│ - Bước 3: Lãng phí điện năng cực lớn (lên tới 30-40%).      │
│ - Bước 2 & 4: Mất 40-60 giờ công tuần tra/tháng mỗi tòa.    │
│                                                             │
│ AI có thể nhảy vào hỗ trợ ở bước nào?                       │
│ - Bước 2, 3, 4: AI Vision (tận dụng camera sẵn có) đếm mật  │
│   độ người theo thời gian thực -> AI Agent tự động điều     │
│   khiển nhiệt độ, lưu lượng gió và chiếu sáng qua BMS/IoT.  │
│                                                             │
│ Đo thành công bằng gì (Metric có số)?                       │
│ - Giảm 20% - 30% tiền điện khu vực công cộng hàng tháng.   │
│ - Giảm 90% thời gian nhân công tuần tra bật/tắt thủ công.   │
│ - 100% không còn sự cố "quên tắt máy lạnh/đèn qua đêm".     │
│                                                             │
│ Quick Architecture: [ ] No AI  [ ] Rule  [ ] LLM  [x] Agent │
│ *(Computer Vision Edge AI + Smart Energy Controller Agent)  │
└─────────────────────────────────────────────────────────────┘
```

`
---

### 💡 Bảng tổng hợp lý do lựa chọn Top 3 (Priority Matrix):

| Card | Subsidiary | Tại sao chọn? (Góc nhìn Lãnh đạo & AI Readiness) |
| :--- | :--- | :--- |
| **#1** | **Vinhomes** | **Fast Win & Net Zero**: Tận dụng hạ tầng camera + BMS sẵn có tại các khu đô thị (Ocean Park, Grand Park...), ROI đo được ngay lập tức trên hóa đơn tiền điện. |
| **#2** | **Vinmec** | **High Value & AI Frontier**: Giải quyết nỗi đau thâm căn cố đế của ngành y (EMR burden), nâng tầm Vinmec thành hệ thống y tế thông minh chuẩn quốc tế (JCI). |
| **#3** | **Xanh SM** | **Hệ sinh thái cộng hưởng**: Bài toán độc nhất vô nhị chỉ có ở Vingroup — giải quyết đồng thời bài toán vận hành taxi điện (GSM) và mạng lưới trạm sạc (V-GREEN). |
