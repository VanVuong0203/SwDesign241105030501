# Lab4 Thiết Kế Ca Sử Dụng cho Hệ Thống "Payroll System"

## 1. Use Case: Login Basic Flow

## Mô tả
Chức năng đăng nhập (Login) cho phép người dùng nhập tên đăng nhập và mật khẩu để xác thực và truy cập vào hệ thống.

---

## Tác nhân (Actors)
- **Any User**: Người dùng bất kỳ muốn đăng nhập vào hệ thống.

---

## Dòng sự kiện (Flow of Events)

### Luồng chính (Main Flow)
1. **Any User** mở giao diện **LoginForm**.
2. **Any User** nhập tên đăng nhập và mật khẩu vào biểu mẫu.
3. **LoginForm** xác thực thông tin:
   - Kiểm tra xem tên đăng nhập và mật khẩu có hợp lệ không.
4. Nếu thông tin hợp lệ:
   - **LoginForm** cấp quyền truy cập vào hệ thống.
5. Nếu thông tin không hợp lệ:
   - **LoginForm** hiển thị thông báo lỗi và yêu cầu nhập lại.

---

## Tiền điều kiện (Preconditions)
- **LoginForm** phải khả dụng.
- Người dùng phải có thông tin đăng nhập hợp lệ trong hệ thống.

## 2. Use Case: Maintain Timecard - Basic Flow

## Mô tả
Chức năng **Maintain Timecard** cho phép nhân viên nhập, cập nhật và lưu thông tin thẻ chấm công, bao gồm số giờ làm việc và mã công việc, để lưu trữ và sử dụng cho các hoạt động quản lý dự án và tính lương.

---

## Tác nhân (Actors)
- **Employee**: Nhân viên cần quản lý thông tin thẻ chấm công.
- **ProjectManagement**: Hệ thống quản lý dự án cung cấp các mã công việc liên quan.
- **EmpData**: Cơ sở dữ liệu quản lý thông tin nhân viên.

---

## Dòng sự kiện (Flow of Events)

### Luồng chính (Main Flow)
1. **Employee** mở giao diện **TimecardForm** để duy trì thông tin thẻ chấm công.
2. **TimecardForm** gửi yêu cầu tới **TimecardController** để hiển thị thông tin thẻ chấm công.
3. **TimecardController** kiểm tra xem thẻ chấm công hiện tại đã tồn tại hay chưa:
   - Nếu chưa tồn tại, tạo một thẻ chấm công mới.
   - Nếu đã tồn tại, lấy dữ liệu thẻ chấm công hiện tại từ **EmpData**.
4. **TimecardController** lấy danh sách mã công việc (Charge Codes) từ **ProjectManagementDatabase**.
5. **Employee** nhập số giờ làm việc và chọn mã công việc liên quan.
6. **TimecardController** cập nhật thông tin thẻ chấm công với dữ liệu từ **Employee** và lưu thay đổi vào **EmpData**.
7. **Employee** lưu thẻ chấm công và nhận xác nhận từ hệ thống.

---

## Tiền điều kiện (Preconditions)
- **Employee** đã đăng nhập và có quyền truy cập vào hệ thống.
- Dữ liệu thẻ chấm công có thể được truy xuất từ cơ sở dữ liệu **EmpData**.

---

## Hậu điều kiện (Postconditions)
- Thông tin thẻ chấm công được cập nhật và lưu thành công trong **EmpData**.
- Dữ liệu thẻ chấm công sẵn sàng cho các quá trình quản lý dự án và tính toán lương.

---

## Trường hợp ngoại lệ (Exceptions)
1. **Thẻ chấm công không thể lưu**:
   - Hệ thống hiển thị thông báo lỗi: `"Không thể lưu thẻ chấm công. Vui lòng thử lại sau."`
2. **Dữ liệu không hợp lệ**:
   - Hệ thống hiển thị thông báo lỗi: `"Dữ liệu nhập không hợp lệ. Vui lòng kiểm tra và nhập lại."`
3. **Không lấy được mã công việc**:
   - Hệ thống hiển thị thông báo lỗi: `"Không thể lấy danh sách mã công việc. Vui lòng liên hệ quản trị viên."`

---

## Biểu đồ hoạt động (Activity Diagram)

![Diagram](https://www.planttext.com/api/plantuml/png/X5H1JiCm4Bpx5QjSW4C_q0EgA70huW0Fs3hRrYYse_M6mjiuy2I-WDkaZKDj4IbI4i-CPsUi_7nzBu8WIsSR9KOQWXKQ9_665sD98zSmWpiCHiDZu_TAeHRFy63RndyI0GQeJY-LQgEKqQP59sV-esTxXAKVyj2bTyA-QOWdXF5pdZO1Jo5_VTwZu1JnpFwDjApGuPOiEJb0rXXwId6r6eAu0EHfbL9dAxFRIJPpy2qvsCH7DSaimOq9pC4E1PtMhczK9hz87iQTmvPasJ576mbdM4rtAI37Wv2ACad7uoc91wCHUA8zo0ckcL2e1hE1sbDmLmBqOO8eY5VUykYa9qUzn0Yvk4sUMEofdsc7lAMbhob4cNBZiqBamwoz31nrydscf2WSlUryn-5GBkYUxJgx9Wx5riO8khQE4MIBI7guG9sBdOWD8xmUqNLIstzZ17pFUIYPBi0dbW-Oeb7jtSQmHJ7UARM8dST_qoy0003__mC0)

## 3. Use Case: Run Payroll - Basic Flow

## Mô tả
Chức năng tính lương (Run Payroll) cho phép hệ thống tự động tính toán và xử lý lương cho nhân viên dựa trên thông tin thời gian làm việc, đơn đặt hàng và phương thức thanh toán đã được cấu hình.

---

## Tác nhân (Actors)
- **System Clock**: Hệ thống tự động kích hoạt quy trình tính lương vào ngày được cấu hình.
- **Printer**: Thiết bị in được sử dụng để in phiếu lương.
- **Bank System**: Hệ thống ngân hàng xử lý giao dịch chuyển khoản.

---

## Dòng sự kiện (Flow of Events)

### Luồng chính (Main Flow)
1. **System Clock** kích hoạt chức năng **SystemClockInterface** để bắt đầu quy trình tính lương.
2. **SystemClockInterface** gửi lệnh chạy quy trình đến **PayrollController**.
3. **PayrollController** kiểm tra xem hôm nay có phải là ngày tính lương hay không.
4. Nếu đúng ngày:
   - **PayrollController** yêu cầu thông tin từ **Employee**:
     - **Employee** lấy thông tin từ **Timecard** và **PurchaseOrder**.
     - **Employee** tính toán lương dựa trên thông tin nhận được.
   - **PayrollController** tạo một đối tượng **Paycheck** với số tiền tương ứng.
   - **PayrollController** xác định phương thức thanh toán:
     - Nếu thanh toán qua séc:
       - **PayrollController** gửi phiếu lương đến **PrinterInterface** để in.
       - **PrinterInterface** gửi lệnh in đến **Printer**.
     - Nếu thanh toán qua chuyển khoản:
       - **PayrollController** lấy thông tin ngân hàng.
       - **PayrollController** gửi giao dịch đến **BankSystem**.
       - **BankSystem** xử lý và gửi giao dịch đến **Bank**.

5. Quy trình hoàn thành.

---

## Tiền điều kiện (Preconditions)
- **System Clock** phải được cấu hình đúng với ngày tính lương.
- Nhân viên phải có thông tin hợp lệ trong hệ thống (Timecard, Purchase Order).
- Phương thức thanh toán của nhân viên phải được thiết lập.

---

## Hậu điều kiện (Postconditions)
- Phiếu lương được in hoặc tiền lương được chuyển khoản thành công.
- Quy trình tính lương hoàn tất và ghi nhận vào hệ thống.

---

## Trường hợp ngoại lệ (Exceptions)
1. **Không phải ngày tính lương**:
   - Quy trình kết thúc mà không thực hiện bất kỳ thao tác nào.
2. **Thông tin nhân viên không đầy đủ**:
   - Hệ thống ghi nhận lỗi và báo cáo.
3. **Lỗi in phiếu lương**:
   - Hiển thị thông báo lỗi và ghi log sự cố.
4. **Lỗi giao dịch ngân hàng**:
   - Hiển thị thông báo lỗi, lưu giao dịch để xử lý lại.

---

## Biểu đồ hoạt động (Activity Diagram)
![Diagram](https://www.planttext.com/api/plantuml/png/X951JiGm34NtEOMNhSG9oc86HYncWQOINC2aBesQEbNY2kLiB3WILy3fC0m3YyacblF-pvVz-VwnJO9HbicRjJ3DKqv2qyu7E-vPAFPegO7riQflJTDYZi7xNM0fDyK6uiBVtKAu7YgNOCRSOTxK80CnL9bIRK1Fyp3DFcHIqrUIPpUHnTZjkGz5l1Bj4ks0YGwnA_QAjOSBu6nXqTl5ev06EEl_HomUcE-ciB1SvoPYUIGPGdU5lKSUBwDZjWFPKPD5qbZmvcG0_FDlT6MolyOxbqvr4f-uudvSXow0k0E9o0cjkC0_y0syA0PEKwYEV2AeE1nddIJCHeMkDskvrLfN_GK00F__0m00)

