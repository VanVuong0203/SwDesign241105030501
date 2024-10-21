# Lab 1: Phân tích kiến trúc và ca sử dụng hệ thống "Payroll System"

## 1. Phân tích kiến trúc

### Đề xuất kiến trúc
Kiến trúc được đề xuất cho hệ thống Payroll là kiến trúc **Layered Architecture** với 3 tầng chính:
- **Tầng Giao diện (UI Layer)**: Chứa các màn hình giao diện người dùng.
- **Tầng Logic (Business Logic Layer)**: Xử lý các yêu cầu từ người dùng và thực hiện các tính toán lương.
- **Tầng Dữ liệu (Data Access Layer)**: Lưu trữ và truy xuất dữ liệu liên quan đến nhân viên, lương, và thời gian làm việc.

### Giải thích lý do lựa chọn
- **Tầng Giao diện (UI Layer)** giúp tách biệt việc hiển thị giao diện người dùng và logic nghiệp vụ.
- **Tầng Logic (Business Logic Layer)** chịu trách nhiệm xử lý các yêu cầu, đảm bảo tính toàn vẹn nghiệp vụ.
- **Tầng Dữ liệu (Data Access Layer)** đảm bảo rằng dữ liệu được truy xuất từ cơ sở dữ liệu một cách hiệu quả.

### Biểu đồ Package mô tả kiến trúc
![Package Diagram](https://www.planttext.com/api/plantuml/png/T95B3e8m48RtdA8Ny08k3F6nS452eXSOouX87wHJ5iHmCXSUoIlO4fwnDDrqllxp_zD-tv-OB1XRIn5Lm4l8aQNG62t4fI6BahqYnjmUu4bMGZU82IXtbAXiTuCnBe1enBFIjP38mMIpadFmoWJjG_jwk_JeSMeqHw92vGkBdXwqiZuccXdRWohFwgx_UmufLfeEEDZLQPx8xJJo4IpSW72o2JpBPhCBJB9bDI6jAm8vHqc0TIPhyPmIkB_PgQCsYb5b_gVT-W400F__0m00)

## 2. Cơ chế phân tích

### Đề xuất các cơ chế cần giải quyết
1. **Cơ chế xác thực người dùng**: Đảm bảo rằng chỉ những người dùng có thông tin hợp lệ mới có thể truy cập vào hệ thống.
2. **Cơ chế quản lý thời gian**: Ghi lại số giờ làm việc của nhân viên và tính toán lương dựa trên thời gian làm việc đó.
3. **Cơ chế thanh toán**: Xác định các phương thức thanh toán và xử lý quy trình thanh toán chính xác.
4. **Cơ chế báo cáo lương**: Hệ thống cần cho phép nhân viên truy cập và xem chi tiết thông tin thanh toán.

## 3. Phân tích ca sử dụng Payment

### Xác định các lớp phân tích
 - Employee: Nhân viên có thể chọn phương thức thanh toán.
 - PaymentController: Quản lý lựa chọn phương thức thanh toán.
 - PaymentMethod: Chứa thông tin về phương thức thanh toán, bao gồm "Pick Up", "Mail", và "Direct Deposit".
 - BankInfo: Nếu chọn phương thức "Direct Deposit", cần thông tin về ngân hàng và tài khoản.
### Biểu đồ tuần tự cho ca sử dụng Payment
![Sequence Diagram](https://www.planttext.com/api/plantuml/png/d591RW8n3BplAtm42NZ07X2qzC01TTMA1qIxXaRhn6bYMktREF0alj14D1NjWgYu9V7CUEp9SN-O1L5UTeOALGjxU3AEk4CiyW76KwXKPz3A8rlnJ8I-X5Sah2LNO8NonatH0vwnJv0INl1zX-4QzNI3yUMkbUSFtI0yEz5i0mmgNRUmTYDOAKqZM6YVN2tGST0olEGd2kVHoeWFZbINzUuQ6WOusKxwlHN9dxS2-gBmoq_UpOEoBIpjXhrHoLbath2MD_F3lDOi0L8zJXFpFYUW_L-0QzSemRloY-UDzkPRucOyyxgr_4dOR35JPj5b-grV0000__y30000)

### Biểu đồ lớp phân tích Payment
![Class Diagram](https://www.planttext.com/api/plantuml/png/X95B2i8m48RtEKMMkkWLf2WkN5W4Jp1DHYtcHJ8HYdWo5nx9AzZMLlf0Ehly-Vduc7a_NsaWy1IrOa9127ohdR8b8hypNar0XO8EK6eqj4UwMBbODZ_EsriXSGtckZCdMwKFrZ86zHPq95-OCwVIOVEEJWBX63n6RAmXRvL2F-ip0-myXpfvbMQWiP-143OQogBEqTU0tqgIP3KLOrFLNkyhygVJER4KZQnFy0400F__0m00)

## 4. Phân tích ca sử dụng Maintain Timecard

### Xác định các lớp phân tích
 - Employee: Nhân viên cập nhật và gửi thông tin thẻ chấm công (timecard).
 - TimecardController: Quản lý việc nhập và gửi thẻ chấm công.
 - Timecard: Chứa thông tin về số giờ làm việc và các dự án mà nhân viên làm việc.
 - ProjectManagementDatabase: Cơ sở dữ liệu dự án quản lý các số dự án để tính công.

### Biểu đồ tuần tự cho ca sử dụng Maintain Timecard
![Sequence Diagram](https://www.planttext.com/api/plantuml/png/Z9DDJiCm48NtFiLSe1V80XMbaM3H2b4ewqay55F_XB6JgcTZmP6u0awWIQ29miwnzTuyVy_vVFzO-e0SAgC55i4nPARKxaGapWjONC63CbGWozJPm4vhuWJkwQqY7xepWJh0nlNVC28RcYMGCc4WsD2nLv6LObntn-wLYh16YtioPCCA0-RegSaIM55DaBuWxwDZPN9YBoObi9YuLLJKIbuOZIMA3cT62QoKBpMUEaz0A_-Qp17DR8Y-DwvY3q-E3pH5eYVuMCg6O4TlRiIsoeqQT3RdlqEjsWbjghRYMritcpyxuoN_GfCnntUr9kzZ2L7mFmoxmP3fDz4dtM9Db_UQx3ckdnMRRo3UAsVdExuk3jOTDSdOwK2tZF6Q_qTy0G00__y30000)

### Biểu đồ lớp phân tích Maintain Timecard
![Class Diagram](https://www.planttext.com/api/plantuml/png/T54xZi8m5Enz2fUxHQwmGcAHQ41Rh4Jzaep0u0yyFqTQhJWP1KVY2ZXH20Y2AsiyRsRU-78wJw8GIt9MLPPYr3Etj-4FqFzAvnDJwOpy6eUAkFxux41u0Sz3ufY1e-edRwHkij3V9D2TU7kxG_3r01WlUjFgh0BlK7VY3LbJPqBl5Qd1cCiqUE5WBRXFoZWanEUeQTzgFO4lImtgFnosg6H1djPmUSySbKgA64o43HfCDyHhB9ChSIjXAAuelaPIgf7WZyntxsyJgKbkilqtTGK00F__0m00)

## 5. Hợp nhất kết quả phân tích

Kết hợp các kết quả phân tích từ hai ca sử dụng trên cho thấy sự tương tác giữa các lớp `Employee`, `Payment`, `Timecard`, và các lớp điều khiển tương ứng (`PaymentController`, `TimecardController`). Hệ thống Payroll yêu cầu sự phối hợp giữa nhiều lớp để xử lý chính xác thông tin liên quan đến lương và thời gian làm việc.

 #### Chức năng chính của hệ thống
 - Quản lý thông tin nhân viên.
 - Tính toán và xuất bảng lương cho nhân viên.
 #### Tương tác giữa các ca sử dụng
 - Quản lý nhân viên là tiền đề để thực hiện tính lương. Thông tin về lương cơ bản từ ca sử dụng 1 sẽ được sử dụng trong ca sử dụng 2 để tính lương.

 ### Viết tài liệu mô tả
 #### Tiêu đề: Tài liệu mô tả hệ thống quản lý lương
 - Giới thiệu: Hệ thống quản lý lương (Payroll System) được thiết kế để hỗ trợ việc quản lý thông tin nhân viên và tính toán lương tự động. Hệ thống này giúp tiết kiệm thời gian và giảm thiểu sai sót trong quá trình tính lương.
 #### Chức năng của hệ thống:
 - Quản lý nhân viên:
   + Thêm, sửa, xóa thông tin nhân viên.
   + Cập nhật thông tin liên hệ và chức vụ của nhân viên.
 - Tính lương
   + Tính toán lương hàng tháng dựa trên số giờ làm việc và lương cơ bản.
   + Xuất bảng lương cho từng nhân viên trong kỳ tính lương.
 #### Luồng công việc

 - Quản lý đăng nhập vào hệ thống.
 - Thêm hoặc sửa thông tin nhân viên.
 - Tính toán lương cho nhân viên dựa trên thông tin đã cập nhật.
 - Xuất bảng lương cho người dùng.

