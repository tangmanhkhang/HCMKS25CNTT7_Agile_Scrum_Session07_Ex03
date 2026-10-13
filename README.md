# KẾ HOẠCH SPRINT 5: TỐI ƯU HÓA TRẢI NGHIỆM VÍ RIKKEIPAY

**Đội ngũ:** RikkeiGo  
**Thời lượng Sprint:** 10 ngày  
**Vai trò đề xuất:** Vy (Developer) & Lan (Scrum Master)  

---

## Phần 1: Phân tích Năng lực & Dự báo Velocity

### 1. Phép tính Planning Capacity (sau khi Hà báo nghỉ 2 ngày)

* **Công thức áp dụng:**
  * Capacity cá nhân = Ngày khả dụng × Giờ tập trung/ngày
  * Planning Capacity = Capacity cá nhân - Việc cố định (Sprint này không trừ Buffer)

* **Cập nhật ngày khả dụng của Hà:**
  * 10 ngày - 2 ngày nghỉ = 8 ngày khả dụng

* **Bảng tính chi tiết Planning Capacity:**

| Developer | Ngày khả dụng | Giờ tập trung/ngày | Capacity cá nhân (giờ) | Việc cố định (giờ) | Planning Capacity (giờ) |
| :--- | :---: | :---: | :---: | :---: | :---: |
| **Tú** | 10 | 6 | 10 × 6 = 60 | 6 (Hỗ trợ vận hành) | 60 - 6 = 54 |
| **Vy** | 10 | 6 | 10 × 6 = 60 | 0 | 60 - 0 = 60 |
| **Khoa** | 9 | 6 | 9 × 6 = 54 | 4 (Họp liên nhóm) | 54 - 4 = 50 |
| **Hà** | 8 | 6 | 8 × 6 = 48 | 0 | 48 - 0 = 48 |
| **Tổng cộng** | **37** | — | **222** | **10** | **212** |

> **Tổng Planning Capacity của đội trong Sprint 5 là 212 giờ.**

---

### 2. Khoảng Velocity dùng để dự báo

* **Dữ liệu lịch sử 4 Sprint gần nhất:** 18, 20, 19, 15 SP (Trung bình = 18 SP; Sprint 4 giảm xuống 15 SP).
* **Năng lực thực tế:** Capacity giảm từ 240 giờ lý thuyết xuống 212 giờ (giảm ~11.6%) do Khoa nghỉ 1 ngày, Hà nghỉ 2 ngày và các đầu việc cố định.
* **Khoảng Velocity dự báo đề xuất:** **15 – 18 Story Points**
  * Đội ưu tiên mốc an toàn **16 SP** để vừa giải quyết dứt điểm nợ kỹ thuật (Integration Test), vừa thích ứng với sự thiếu hụt nhân sự.

---

## Phần 2: Thiết kế Phạm vi Sprint & Sprint Goal

### 1. Sprint Goal

> **"Khách hàng có thể thanh toán chuyến đi và nhận tiền hoàn tự động vào ví RikkeiPay minh bạch, thông suốt khi chuyến bị hủy."**

*(Sprint Goal tập trung vào Outcome: giải quyết dứt điểm lỗi thanh toán và phản hồi của người dùng về việc nhận lại tiền khi hủy chuyến).*

---

### 2. Danh sách PBI chọn vào Sprint 5

Tổng số Story Point cam kết: **16 SP** (nằm trọn vẹn trong khoảng dự báo 15 – 18 SP).

| Thứ tự | PBI | SP | Lý do chọn |
| :---: | :--- | :---: | :--- |
| **1** | Thanh toán chuyến đi bằng ví RikkeiPay | 8 | Trọng tâm Sprint Goal; giải quyết lỗi khách phàn nàn và bổ sung Integration Test để hoàn thành Definition of Done (DoD). |
| **2** | Hoàn tiền vào ví khi chuyến bị hủy | 5 | Trực tiếp phục vụ Sprint Goal; xử lý bức xúc của khách hàng khi chuyến bị hủy mà không biết tiền đã về ví chưa. |
| **3** | Xem số dư và lịch sử giao dịch ví | 3 | Hỗ trợ Sprint Goal; giúp khách hàng tự kiểm tra, đối soát được tiền ra (thanh toán) và tiền vào (hoàn tiền) trên ứng dụng. |

---

### 3. Lý do không chọn các PBI còn lại (1 câu/PBI)

* **PBI 4 (Gửi SMS khi tài xế sắp đến - 3 SP):** Không chọn vì chưa ký hợp đồng với nhà cung cấp SMS, vi phạm Definition of Ready (DoR) và có rủi ro bị chặn bởi bên thứ ba.
* **PBI 5 (Giao diện chủ đề Tết - 2 SP):** Không chọn vì không đóng góp vào Sprint Goal của ví RikkeiPay và đội không áp dụng bẫy nhồi nhét việc ngoài luồng cho vừa khít số SP trống.
* **PBI 6 (Chat với tài xế - 5 SP):** Không chọn vì không liên quan đến mục tiêu ví điện tử và nếu nhận thêm sẽ nâng tổng lên 21 SP, vượt quá Capacity thực tế của đội.

---

## Phần 3: Phân rã Task cho PBI "Hoàn tiền vào ví khi chuyến bị hủy"

PBI được chia thành 3 task kỹ thuật với đầu ra kiểm chứng được (Verifiable Output):

### Task 1: Xây dựng API xử lý nghiệp vụ hoàn tiền vào ví (Backend)
* **Nội dung công việc:**
  * Lắng nghe sự kiện hủy chuyến từ Ride Service.
  * Kiểm tra điều kiện hoàn tiền và ghi nhận giao dịch cộng tiền vào số dư ví của khách hàng.
  * Đảm bảo tính Idempotency để ngăn chặn lỗi hoàn tiền trùng lặp (Double Refund).
* **Đầu ra kiểm chứng được:** API endpoint hoàn tiền vượt qua 100% các Unit Test kịch bản hủy chuyến và mã nguồn được merge vào nhánh chính sau khi pass Code Review.

---

### Task 2: Cập nhật giao diện hiển thị trạng thái hoàn tiền trên màn hình hủy chuyến (Frontend/Mobile)
* **Nội dung công việc:**
  * Hiển thị trạng thái giao dịch hoàn tiền trực quan: *"Đang xử lý hoàn tiền"* hoặc *"Đã hoàn [số tiền] vào ví RikkeiPay"*.
  * Gắn liên kết điều hướng trực tiếp sang màn hình Lịch sử giao dịch ví.
* **Đầu ra kiểm chứng được:** Bản build ứng dụng (APK/TestFlight) hiển thị đúng mẫu giao diện Figma và cập nhật chính xác trạng thái hoàn tiền theo dữ liệu API trả về.

---

### Task 3: Viết và thực thi kịch bản Integration Test luồng thanh toán - hủy chuyến - hoàn tiền
* **Nội dung công việc:**
  * Thiết lập kịch bản tích hợp: Đặt xe thành công $\rightarrow$ Trừ tiền ví $\rightarrow$ Hủy chuyến $\rightarrow$ Tiền tự động hoàn về ví $\rightarrow$ Hệ thống ghi nhận biến động số dư.
  * Kiểm thử các trường hợp mạng chập chờn hoặc timeout giữa hệ thống cuốc xe và ví.
* **Đầu ra kiểm chứng được:** Báo cáo kiểm thử tích hợp (Automation/Integration Test Report) đạt trạng thái Pass cho luồng hủy chuyến và số dư ví khớp hoàn toàn trên hệ thống.