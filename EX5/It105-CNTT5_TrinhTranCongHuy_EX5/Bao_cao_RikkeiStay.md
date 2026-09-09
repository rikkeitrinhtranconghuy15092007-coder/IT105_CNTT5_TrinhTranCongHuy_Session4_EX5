# Báo cáo Khảo sát và Phân tích Hệ thống Khách sạn RikkeiStay

## Bước 1: Nhận diện 5 thành phần HTTT và Phân biệt Dữ liệu vs Thông tin

### 1. Bổ sung 5 thành phần HTTT

| Thành phần HTTT | Ví dụ thực tế tại RikkeiStay | Vai trò cơ bản |
| :--- | :--- | :--- |
| **1. Phần cứng** | Máy Kiosk tự làm thủ tục tại sảnh, khóa cửa từ thông minh | Thiết bị vật lý cấp thẻ phòng và nhận diện |
| **2. Phần mềm** | Phần mềm quản trị khách sạn PMS, ứng dụng di động RikkeiStay | Quản lý đặt phòng, sơ đồ buồng phòng và thanh toán |
| **3. Dữ liệu** | Trạng thái phòng (Trống/Đã đặt/Đang dọn), thông tin hộ chiếu khách | Dữ liệu lưu trú và phục vụ |
| **4. Con người** | Khách lưu trú (Guest), Nhân viên Lễ tân, Quản lý buồng phòng | Người sử dụng dịch vụ và người vận hành hệ thống |
| **5. Quy trình** | Quy trình đặt phòng trực tuyến, quy trình Check-in tự động tại Kiosk | Các bước tiếp đón, nhận phòng, phục vụ và trả phòng |

### 2. Phân loại Dữ liệu và Thông tin

| STT | Nội dung dữ liệu tại RikkeiStay | Dữ liệu | Thông tin | Lý do phân loại |
| :--- | :--- | :--- | :--- | :--- |
| 1 | 302 | [ x ] | [ ] | Chuỗi số thô, chưa rõ là số phòng, số tiền hay mã khách |
| 2 | Phòng Deluxe 302 đã được dọn sạch và sẵn sàng đón khách lúc 13:30 | [ ] | [ x ] | Đầy đủ ngữ cảnh: Loại phòng, Số phòng, Trạng thái, Thời gian |
| 3 | VIP2025 | [ x ] | [ ] | Chuỗi ký tự thô, chưa rõ là mã voucher hay hạng thẻ khách hàng |
| 4 | Tỷ lệ lấp đầy phòng trong kỳ nghỉ lễ 30/04 đạt 98% trên toàn hệ thống | [ ] | [ x ] | Số liệu đã qua tính toán tổng hợp, có ý nghĩa đánh giá hiệu quả kinh doanh trong một thời điểm cụ thể. |
| 5 | KH05, John Smith, UK, 3 đêm | [ x ] | [ ] | Các giá trị thuộc tính thô, rời rạc về một khách hàng, chưa kết nối thành câu có bối cảnh đầy đủ. |

## Bước 2: Khảo sát môi trường và Xác định Stakeholders

### 1. Khảo sát môi trường

| Yếu tố khảo sát tại RikkeiStay | Thuộc loại môi trường | Tầm ảnh hưởng đến hệ thống |
| :--- | :--- | :--- |
| Trình độ ngoại ngữ và kỹ năng tin học của nhân viên lễ tân | Môi trường Nội bộ | Phần mềm cần hỗ trợ đa ngôn ngữ và thao tác nhanh chóng |
| Quy định khai báo tạm trú cho khách quốc tế của Công an địa phương | Môi trường Bên ngoài | Hệ thống bắt buộc phải tích hợp tính năng gửi dữ liệu lưu trú |
| Sự cạnh tranh về giá và dịch vụ từ các nền tảng OTA quốc tế | Môi trường Bên ngoài | Thúc đẩy hệ thống đồng bộ lịch phòng tự động tránh bị trùng lặp |
| Thói quen sử dụng thanh toán không tiền mặt của du khách quốc tế | Môi trường Bên ngoài | Yêu cầu Kiosk/App phải tích hợp đa dạng cổng thanh toán quốc tế (Visa/Mastercard, Apple Pay, v.v.). |
| Chất lượng hệ thống mạng Wi-Fi phủ sóng tại từng tầng khách sạn | Môi trường Nội bộ | Quyết định tính ổn định và khả năng đồng bộ dữ liệu theo thời gian thực của app dọn phòng trên điện thoại. |

### 2. Xác định Stakeholders

| Nhóm Stakeholder | Vai trò trong dự án | Mối quan tâm lớn nhất đối với phần mềm |
| :--- | :--- | :--- |
| 1. Khách lưu trú (Guest) | Người sử dụng dịch vụ | Nhận phòng nhanh chóng tại Kiosk không phải xếp hàng chờ đợi |
| 2. Nhân viên Lễ tân (Front Desk) | Người trực quầy tiếp đón | Nắm rõ trạng thái từng phòng trên sơ đồ trực quan theo thời gian thực |
| **3. Quản lý buồng phòng (Housekeeping)** | Người điều phối nghiệp vụ phòng | Nhận thông báo tự động khi khách check-out để phân công dọn dẹp kịp thời và dễ theo dõi năng suất nhân viên. |

## Bước 3: Lựa chọn kỹ thuật thu thập yêu cầu

### 1. Kỹ thuật khảo sát

| STT | Tình huống khảo sát tại RikkeiStay | Kỹ thuật phù hợp nhất | Lý do lựa chọn ngắn gọn |
| :--- | :--- | :--- | :--- |
| 1 | Quan sát thực tế nhân viên dọn dẹp phòng để nắm quy trình... | Quan sát hiện trường | Thấy trực tiếp các bước thao tác thực tế tại hiện trường |
| 2 | Thu thập đánh giá từ hơn 5.000 du khách sau khi trả phòng... | Bảng câu hỏi (Survey) | Số lượng khách lớn, thu thập nhanh số liệu đánh giá chất lượng |
| 3 | Phỏng vấn Tổng Giám đốc khách sạn về kế hoạch mở rộng chuỗi... | Phỏng vấn (Interview) | Đối tượng cấp cao, số lượng ít, cần trao đổi sâu về định hướng chiến lược. |
| 4 | Đọc quy chế định mức thời gian dọn phòng và bảng giá đồ uống... | Nghiên cứu tài liệu | Bảng quy chế và đơn giá đã được ban hành chính thức có sẵn |
| 5 | Lấy ý kiến của nhóm 10 nhân viên lễ tân ca đêm về các tình huống... | Thảo luận nhóm | Số lượng nhân sự vừa phải, cùng chuyên môn, dễ dàng trao đổi tương tác để tìm ra giải pháp chung. |

### 2. Câu hỏi phỏng vấn mở dành cho Nhân viên lễ tân
*"Những khó khăn hay sự cố phổ biến nhất mà bạn thường gặp khi làm thủ tục nhận phòng cho khách vào giờ cao điểm là **những lỗi gì liên quan đến thao tác trên phần mềm, thiết bị quét giấy tờ tùy thân hay quá trình đối soát thanh toán?**"*

## Bước 4: Phân loại Yêu cầu (FR và NFR)

| STT | Phát biểu yêu cầu | Phân loại | Mã định danh | Câu hỏi cốt lõi giải thích |
| :--- | :--- | :--- | :--- | :--- |
| (1) | Khách hàng có thể chọn ngày nhận phòng và loại phòng trên trang web | FR | FR-01 | Tính năng đặt phòng hệ thống cung cấp (LÀM GÌ) |
| (2) | Thủ tục quét hộ chiếu và cấp thẻ phòng tại máy Kiosk tự động dưới 1 phút | NFR | NFR-01 | Tiêu chuẩn tốc độ phục vụ tự động (TỐT NHƯ THẾ NÀO) |
| (3) | Dữ liệu thông tin cá nhân và hộ chiếu của du khách phải được bảo mật | NFR | NFR-02 | Tiêu chuẩn an toàn thông tin cá nhân (TỐT NHƯ THẾ NÀO) |
| (4) | Nhân viên buồng phòng có thể cập nhật trạng thái phòng đã dọn xong trên điện thoại | FR | FR-02 | Là tính năng, chức năng thao tác cụ thể mà ứng dụng cung cấp (LÀM GÌ). |
| (5) | Hệ thống quản lý lịch phòng phải đồng bộ theo thời gian thực 24/7 tránh trùng phòng | NFR | NFR-03 | Tiêu chuẩn về tính sẵn sàng, tin cậy và đồng bộ dữ liệu (TỐT NHƯ THẾ NÀO). |

## Bước 5: Đặc tả User Story

* **Là một (Who):** Du khách lưu trú tại khách sạn RikkeiStay
* **Tôi muốn (What):** Tự làm thủ tục nhận phòng và lấy thẻ khóa phòng tại máy Kiosk tự động
* **Để (Why):** Không phải xếp hàng chờ đợi lâu ở quầy lễ tân sau một chuyến đi dài mệt mỏi, giúp tiết kiệm thời gian, tăng sự chủ động và có trải nghiệm riêng tư, thoải mái hơn.
