# Lab5 Thiết Kế Hệ Thống Con Trong Hệ Thống "Payroll System"

## 1. Use Case Realization - Run Payroll

## Mô tả
Chức năng tính lương (Run Payroll) cho phép hệ thống tự động tính toán và xử lý lương cho nhân viên dựa trên thông tin thời gian làm việc, đơn đặt hàng và phương thức thanh toán đã được cấu hình.

---

## Tác nhân (Actors)
- **System Clock:** Hệ thống tự động kích hoạt quy trình tính lương vào ngày được cấu hình.

- **Printer:** Thiết bị in được sử dụng để in phiếu lương.

- **Bank System:** Hệ thống ngân hàng xử lý giao dịch chuyển khoản.
---

## Dòng sự kiện (Flow of Events)

### Luồng chính (Main Flow)
1. **System Clock :** kích hoạt chức năng **SystemClockInterface** để bắt đầu quy trình tính lương.

2. **SystemClockInterface:** gửi lệnh chạy quy trình đến **PayrollController**.

3. **PayrollController:** kiểm tra xem hôm nay có phải là ngày tính lương hay không.

4. **Nếu đúng ngày:**

- **PayrollController** yêu cầu thông tin từ **Employee**:

  - **Employee** lấy thông tin từ **Timecard** và **PurchaseOrder**.

  - **Employee** tính toán lương dựa trên thông tin nhận được.

- **PayrollController** tạo một đối tượng **Paycheck** với số tiền tương ứng.

- **PayrollController** xác định phương thức thanh toán:

  - **Nếu thanh toán qua séc:**

    - **PayrollController** gửi phiếu lương đến **PrinterInterface** để in.

    - **PrinterInterface** gửi lệnh in đến **Printer**.

  - **Nếu thanh toán qua chuyển khoản:**

    - **PayrollController** lấy thông tin ngân hàng.

    - **PayrollController** gửi giao dịch đến **BankSystem**.

    - **BankSystem** xử lý và gửi giao dịch đến **Bank**.

5. **Quy trình hoàn thành**.
---

## Tiền điều kiện (Preconditions)
- **System Clock** phải được cấu hình đúng với ngày tính lương.

- Nhân viên phải có thông tin hợp lệ trong hệ thống (Timecard, Purchase Order).

- Phương thức thanh toán của nhân viên phải được thiết lập.

## Hậu điều kiện (Postconditions)
- Phiếu lương được in hoặc tiền lương được chuyển khoản thành công.

- Quy trình tính lương hoàn tất và ghi nhận vào hệ thống.

---

## Trường hợp ngoại lệ (Exceptions)
1. **Không phải ngày tính lương:**

    - Quy trình kết thúc mà không thực hiện bất kỳ thao tác nào.

2. **Thông tin nhân viên không đầy đủ:**

    - Hệ thống ghi nhận lỗi và báo cáo.

3. **Lỗi in phiếu lương:**

    - Hiển thị thông báo lỗi và ghi log sự cố.

4. **Lỗi giao dịch ngân hàng:**

    - Hiển thị thông báo lỗi, lưu giao dịch để xử lý lại.

---
  
## Biểu đồ hoạt động (Activity Diagram)

![Diagram](https://www.planttext.com/api/plantuml/png/T591Rjim4Bph5NkCls0T6iI79d21Ed0-mD2qI5XQkHGLHESUSyeBQiV88MaD671E8W8V6FWVV46_qALaEqRQNaHXEJCxiylVTdDQ6APDcQLHynDr-sx99SZSrtC3rzx-K32i2YCowAKvdyI4KDv-py1e1hTKbkub0sGLSBU6gVJrGW4cRbQ1SKkKa6vNspacSQJ6S7A-1wTkzY_KfmuOAH1EUcxTYG2wNtpzI1XgWWaOXO3IFI3SAFUCOBpz2LSg4vpf4ToGvA3KNB92VDKZeUCWSDN8czpDyTrAg5F07DxklRrNOBOhRnVKOS0gBaM8IP2Ze5FPKic9jq-S3hPN3T0GRV1_o27Lq3tn48l4FtkxLAIhVBqfzyw2dtg3CD0AZT0NuJDcNCGjvm8_4iA5I0j10vDbHNOH9c5t2zor-Nj-IPYVTBEMV72IA9R3oDixslxEnHd3IRlx7VAz0BT4eYM-7lCQCpXIuwYrr6-wDcliaw09DceEtqeofDql948BBqm-ZQBkvU62tXyPfFtMZoQEJWaLNkWV0000__y30000)
