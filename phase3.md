# 3.2. Problem Statement (6-field)
## Vin Smart Future Standard — Xanh SM

> **Tóm tắt bài toán:** Chuyên viên Vận hành/CSKH cần xác minh nhanh các khiếu nại liên quan đến hủy chuyến, câu giờ và sai điểm đón bằng cách tổng hợp hội thoại, GPS và trạng thái cuốc xe. AI sẽ tạo bản tóm tắt bằng chứng và đề xuất kết luận để nhân viên phê duyệt.

| Field | Nội dung |
|---|---|
| **1. Actor / Operator** | **Chuyên viên Vận hành & Chăm sóc Khách hàng (Operations/CSKH)** thuộc Xanh SM là người xử lý và phê duyệt vụ việc. **Khách hàng đặt xe** và **tài xế** là các bên liên quan trực tiếp. |
| **2. Current Workflow** | Khi khách hàng khiếu nại hoặc tự hủy chuyến, nhân viên: **(1)** mở lịch sử cuốc xe và log GPS; **(2)** nghe lại file ghi âm/đọc chat giữa khách và tài xế; **(3)** đối chiếu hội thoại với vị trí, thời gian và trạng thái cuốc xe; **(4)** phân loại vi phạm, tổng hợp chứng cứ và ra quyết định xử phạt/hoàn phí. Hiện tại, cả 4 bước đều được thực hiện thủ công. |
| **3. Bottleneck** | **Bước 3–4**, mất khoảng **10–15 phút/lượt**. Nhân viên phải nghe/đọc lại toàn bộ nội dung hội thoại, sau đó đối chiếu thủ công với tọa độ GPS theo từng mốc thời gian để xác định tài xế có câu giờ, đi sai điểm đón hoặc gây áp lực khiến khách hủy chuyến hay không. |
| **4. Business Impact** | Quy trình kéo dài làm tăng chi phí vận hành và số vụ tồn đọng; khách hàng phải chờ lâu, dễ phát sinh trải nghiệm tiêu cực và rời bỏ dịch vụ; tài xế có thể lách quy định để trục lợi hoặc né KPI tỷ lệ hủy; doanh thu bị thất thoát và uy tín thương hiệu gọi xe bị ảnh hưởng. |
| **5. Success Metric** | **Efficiency:** Giảm thời gian xác minh một vụ từ **10–15 phút xuống dưới 1 phút**. <br><br> **Customer Experience:** Giảm **15%** tỷ lệ khách tự hủy chuyến do chờ lâu so với baseline trước triển khai. <br><br> **Quality:** Độ chính xác nhận diện hành vi vi phạm của tài xế đạt **≥ 90%**, đo trên tập vụ việc đã được nhân viên vận hành kiểm duyệt. |
| **6. Operational Boundary** | **AI được phép:** truy xuất log GPS của cuốc xe, dữ liệu chat in-app và bản phiên âm (STT) của cuộc gọi qua app; trích xuất các mốc thời gian và bằng chứng liên quan; dựng timeline; phân loại dấu hiệu vi phạm; tạo **draft verdict** gồm lý do, bằng chứng và đề xuất xử phạt/hoàn phí. <br><br> **AI bị cấm:** tự ý trừ tiền, khóa tài khoản tài xế, từ chối khiếu nại hoặc phát hành quyết định cuối cùng. Mọi quyết định phải được nhân viên Operations/CSKH phê duyệt (**bắt buộc Human-in-the-loop — HITL**). Dữ liệu âm thanh, hội thoại và vị trí phải được bảo vệ theo chính sách bảo mật nội bộ. |

## Workflow đề xuất có AI hỗ trợ

```text
Khiếu nại / tự hủy chuyến
        ↓
AI gom dữ liệu: GPS + trạng thái cuốc + chat + STT cuộc gọi
        ↓
AI dựng timeline và trích xuất bằng chứng liên quan
        ↓
AI phân loại dấu hiệu: câu giờ / sai điểm đón / ép hủy / chưa đủ bằng chứng
        ↓
AI tạo draft verdict và hiển thị nguồn bằng chứng
        ↓
Nhân viên Operations/CSKH kiểm tra → phê duyệt hoặc chỉnh sửa kết luận
        ↓
Hệ thống mới thực hiện xử lý theo quyết định đã được duyệt
```

## Điều kiện chất lượng và an toàn

- Mỗi kết luận phải đi kèm **timeline, dữ liệu nguồn và mức độ tin cậy** để nhân viên có thể kiểm tra.
- Nếu thiếu dữ liệu, dữ liệu mâu thuẫn hoặc độ tin cậy dưới ngưỡng cấu hình, AI phải chuyển vụ việc sang **manual review**, không tự suy diễn.
- Không sử dụng bản ghi âm, nội dung chat hoặc dữ liệu GPS ngoài mục đích xác minh vụ việc được phân quyền.
- Lưu lại lịch sử chỉnh sửa và quyết định phê duyệt của nhân viên để phục vụ audit, khiếu nại và cải thiện mô hình.
