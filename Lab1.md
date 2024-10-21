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
### Biểu đồ tuần tự cho ca sử dụng Select Payment
![Sequence Diagram](https://www.planttext.com/api/plantuml/png/h9EnIiD07CRtFCL_hD2-G0OfPb11YvFe96SQUqVJ_yLu9tHsS1079rUZ5B5GhE1YRkXmqlUu9_0Ll6j0WcreGBDS4kxx-7tt_-vBpTeNWgH23cAFX8AdqA7w4KyEcHwZLtg7rYOSaE4WGX5m52cFuoZr8Q16tI8aT3wTPzW3ORzVGhiGf22upj1RKfMizYD1UTU7OpsM49hyMTQnAbJGga2ILcozHWa8_J64i41iTAZ99mZ2v1bR_BnlmhPH4mRdai3fV2hXyuuPTOrD6qiEZRf2w5DkyYUhIerwip3CvBDaOrKc2rCwBXzssCB0fRWfW_pBeKBZKa-WQzJ8NyjAOh5cZmVB5F0xJsb4WkftXyKGi6Ut0DKFsBCkDQALXbFbif9bYs1_5y-u3tjkKex_jSeYmcwjrWMs40cWwuNuU--ET1OMPkWI_ZZNAKkbjcspkBjfdsy0003__mC0)

### Biểu đồ lớp phân tích Select Payment
![Class Diagram](https://www.planttext.com/api/plantuml/png/UhzxlqDnIM9HIMbk3bToJc9niO9Vnk55UV5XcOTNvIbKSoa0GNB6mzszUG4PnpOSMvYN7WBahKmEoKZComZ9FxmmJqCJegWqBztvuQwb1I4PXxS0LMNc-QK33V8ul20l7QYabWjgF2vZe7O5bnHbvgKhvEG_tBKm4sBmmrrh2_moW6G97YV0pNTwk7lcaGcP3tStbdfd0AdcF0mxYFCFQTPYyJMgZqg0uOcGGvOfVhXxOiZX1PdU6K1FByu3cOaS1xgwTdWznONNno3TkDnFM2SMNt4vfEQbW58B5nS0003__mC0)

## 4. Phân tích ca sử dụng Maintain Timecard

### Xác định các lớp phân tích
 - Employee: Nhân viên cập nhật và gửi thông tin thẻ chấm công (timecard).
 - TimecardController: Quản lý việc nhập và gửi thẻ chấm công.
 - Timecard: Chứa thông tin về số giờ làm việc và các dự án mà nhân viên làm việc.
 - ProjectManagementDatabase: Cơ sở dữ liệu dự án quản lý các số dự án để tính công.

### Biểu đồ tuần tự cho ca sử dụng Maintain Timecard
![Sequence Diagram](https://www.planttext.com/api/plantuml/png/h5H1IiD05DtFAVu5Ue4kf5YXGaD16aHN4gCaWycqj9c2o-B2XHjTYKYnjOXGA5fqbK5SZFGUSmAlu9-fO6W2dHOtap3pyzxxx_t9j_YiT1Ela_0u8fwVj3hG2EKZEzgdSi98vXrAMx2jnDtNDLMYp-iXFYwO6wfKu286j4OzLeP3EU7Wg_IPGwBFz8g74E0fyQ84wg5yPm7uygsW05PJQ1qvLbUberOU3s8bxYavPIV42hSw7pMLUDXHuiN1cak-nrKwPexymAsPx2EJezAdS-WgSGEn74Cxb5EoyZCesPbNvTePP6WlCLYeHuPCMcNODMN6ZQi2PtfokCInVjODt9Z-IWsmP02H7CRGqnxuTexdBJ2GJ2Cd1GEoliYQ4bDQWBIPl0CvyWtCpC_qRGQx-MV3sMB6iMpSXWZTi1livGZT1SonnDb6b5kACF-HKaQNzTN8mJhprw8hNjIKXKZZgqcTGQ0JssJayo0Lx4__sGZv0G00__y30000)

### Biểu đồ lớp phân tích Maintain Timecard
![Class Diagram](https://www.planttext.com/api/plantuml/png/d5B1IiCm6BxdANBKGrz1XXDsi1P5yIeroXhimbWJi8Y7uS7hUlGWRXOH1cNkcY0x_6NlyJ-1hs1IfnIf5CmXWU___k__lYGVPjL9P3YIQX0J5eT9GeC8diNPAOUve3U4sjL7K_2J2BMnctdaFHwAhUsg92nQ37lSmXQv9HkDN-HAnwD17wOfFKUzaBJCKB-g6do5UYMfZ42p2kL2qWHDLccN4yXzc0wgcTSmOqvxoJOculMRga_VHVDGJcpVMEr7zhWJJNueJM6kkiv6SpRceWKke6mc_74lFpwwwzancgSzD0lVshXNHmfrBdnujz0Injy-OjGlgMLc1v0VHb1yQTJVmVDssbEHzjnEvtzThLb8vr9Sk5z4o2S0003__mC0)

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

