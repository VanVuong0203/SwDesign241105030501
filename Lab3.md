# Lab 3: Xác định các phần tử thiết kế của hệ thống “Payroll System”

## 1. Subsystem context diagrams

### Hệ thống BankSystem
![Sequence Diagram](https://www.planttext.com/api/plantuml/png/R90nIWGn58RxdE8t_Lx0GbQ7ORSGaT4BX9cu2PjvMIOPOH0h2y-XOYE8ZTMci9YJv0HUmSngP45JlRplVVoFzna-viwBplUjOGUDlD8aKPN5vV7PuhH4ROHpZ8dQsmxyN0oTDGONW_EovH0EFwqyKROROmSfTon_CbnM--QoOfsilQ2LaU0dWjQ_z8OXlPmscnrXmjyKX-2B65url1hVQGMlAPM25BmT7uZltBtvIS-RJ7AX-Y66Ey9QsRXz-aTEU_xDBFgKLSVjymPD36ymEeRx7gJ6HyAr7b-IVClcafhfaenz0G00__y30000)

#### Giải thích các thành phần:
- Payroll System: Hệ thống trả lương gửi các thông tin thanh toán cho Bank System để thực hiện chuyển khoản.
- Employee: Người lao động nhận thanh toán từ Bank System qua tài khoản ngân hàng của họ.
- HR System: Cung cấp thông tin về nhân viên cho Bank System như thông tin tài khoản ngân hàng và các khoản khấu trừ.

#### Mô tả

BankSystem chịu trách nhiệm xử lý các giao dịch tài chính và chuyển khoản lương cho nhân viên. Nó tiếp nhận thông tin từ Payroll System về các khoản thanh toán và chuyển khoản trực tiếp vào tài khoản ngân hàng của nhân viên.

#### Interface:

- processPayment(employeeId: String, amount: Double): Boolean
Mục đích: Xử lý việc chuyển khoản lương cho nhân viên.
Input: employeeId (ID của nhân viên), amount (số tiền cần chuyển).
Output: Trả về true nếu giao dịch thành công, false nếu thất bại.

- getEmployeeBankDetails(employeeId: String): BankDetails
Mục đích: Lấy thông tin tài khoản ngân hàng của nhân viên.
Input: employeeId (ID của nhân viên).
Output: Trả về đối tượng BankDetails, chứa thông tin tài khoản ngân hàng của nhân viên.

- updateBankTransaction(transactionId: String, status: String): Boolean
Mục đích: Cập nhật trạng thái giao dịch (thành công hoặc thất bại).
Input: transactionId (ID của giao dịch), status (trạng thái giao dịch).
Output: Trả về true nếu cập nhật thành công, false nếu không.

### Hệ thống PrintService
![Sequence Diagram](https://www.planttext.com/api/plantuml/png/UhzxlqDnIM9HIMbk3fTYIcfQPbwgGf2hSuYZdxkFgq9oJc9nCHTNOd99Vf62Ka1YPL5-Jev2S6LnIMgkaa9YiG9K2AR2DRSW9xyoDHKi1-F093s2a7Lw174LfIQN9EQbvwG2ZIxAp2jH24ujAijC1kgkvb800fXzkhfs2c05K7a5AmKbzuUxrsOg91rUcA-G329oZcqujZ0lNU78n8UxcnKoyvJ09W2jnARPkHIeCldXhgK52YaFTwzNoCbykBkzL24lu_2YF8MopCEheDfHz84CWda9pP2aXxiM0pamDvGTNe1mcH9NBPT3QbuAA82vk000003__mC0)

#### Giải thích các thành phần:
- Payroll System: Gửi các báo cáo lương, bảng lương, và các thông tin thanh toán khác cho PrintService để in.
- HR System: Cung cấp thông tin nhân viên cần in, chẳng hạn như danh sách nhân viên và các khoản thanh toán cá nhân.
- Employee: Nhận bảng lương hoặc các tài liệu in ấn khác từ PrintService.
- PrintService: Hệ thống in ấn thực hiện việc in các báo cáo, bảng lương, hoặc các tài liệu liên quan đến việc trả lương cho nhân viên.

#### Mô tả

PrintService chịu trách nhiệm in các báo cáo, bảng lương, và các tài liệu liên quan đến việc thanh toán lương cho nhân viên. Nó nhận dữ liệu từ Payroll System và HR System để tạo ra các bản in báo cáo.

#### Interface:

- generatePayrollReport(employeeId: String, payrollData: PayrollData): Boolean
Mục đích: Tạo báo cáo lương cho một nhân viên.
Input: employeeId (ID của nhân viên), payrollData (Dữ liệu bảng lương của nhân viên).
Output: Trả về true nếu báo cáo được tạo thành công, false nếu có lỗi xảy ra.

- printDocument(documentId: String): Boolean
Mục đích: In một tài liệu cụ thể.
Input: documentId (ID của tài liệu cần in).
Output: Trả về true nếu in thành công, false nếu có lỗi xảy ra.

- getPrintStatus(printJobId: String): String
Mục đích: Kiểm tra trạng thái của một công việc in.
Input: printJobId (ID công việc in).
Output: Trả về trạng thái của công việc in (ví dụ: "Đang in", "Hoàn thành", "Lỗi").

### Hệ thống ProjectManagementDatabase subsystems.
![Sequence Diagram](https://www.planttext.com/api/plantuml/png/d99BJiCm48RtFiMGVI_00XMLY2ueAe4B38b9KZdZAfuWHOWrr-0XrgWIgqQ8XK-I4t05d0P7HQ92gbVp-FtDFxA_ci-nOIovAfGuIEHDJXAYS79rV7vw5aAiq1WXC6PTGZ37kjHAmMLjM1O1e86VabU4nLBfMifDpoU-EOssRqwZ0LlgXOmPPaYOoa8Iz-Y-F4iB5gKBa58b_rB32J9Uet5JxmIuutsEHaS3PL1xCHn2CAaeXRXTlow1C_lk4ix9XKWPiBPF56nuplYUAChiCu5fcrLFsjhfV-H5rQvV29JzWAHjta3bRVDGTV4A1c-x2HtVFy5kXvu6j_Rnz-RtOYmfwVx5Dm000F__0m00)

#### Giải thích các thành phần:
- Payroll System: Gửi thông tin chi trả (lương, chi phí dự án) cho ProjectManagementDatabase để ghi nhận và cập nhật thông tin thanh toán cho nhân viên tham gia dự án.
- HR System: Cung cấp thông tin về nhân viên cho ProjectManagementDatabase, chẳng hạn như nhân viên nào tham gia dự án, vai trò và mức lương của họ.
- Project Management: Quản lý các dự án, cung cấp các chi tiết về dự án như ngân sách, tiến độ, nguồn lực, và các khoản chi phí liên quan.
- ProjectManagementDatabase: Hệ thống cơ sở dữ liệu chịu trách nhiệm lưu trữ và quản lý thông tin về các dự án, nhân viên tham gia, và các khoản thanh toán, cũng như các dữ liệu liên quan đến tiến độ và chi phí dự án.
- Employee: Nhận thông tin về các dự án mà họ tham gia và nhận thanh toán từ ProjectManagementDatabase.

#### Mô tả

ProjectManagementDatabase lưu trữ và quản lý các thông tin liên quan đến các dự án, bao gồm các dữ liệu về nhân viên, tiến độ, ngân sách, và các khoản thanh toán cho dự án. Hệ thống này giúp theo dõi các dự án và các khoản thanh toán chi tiết liên quan đến dự án.

#### Interface:

- addProject(project: Project): Boolean
Mục đích: Thêm một dự án mới vào cơ sở dữ liệu.
Input: project (Đối tượng chứa thông tin về dự án).
Output: Trả về true nếu dự án được thêm thành công, false nếu có lỗi.

- getProjectDetails(projectId: String): Project
Mục đích: Lấy thông tin chi tiết của một dự án.
Input: projectId (ID của dự án).
Output: Trả về đối tượng Project, chứa các chi tiết về dự án.

- getProjectPayments(projectId: String): List<Payment>
Mục đích: Lấy thông tin về các khoản thanh toán cho một dự án.
Input: projectId (ID của dự án).
Output: Trả về một danh sách các đối tượng Payment chứa thông tin về các khoản thanh toán.

- updateProjectStatus(projectId: String, status: String): Boolean
Mục đích: Cập nhật trạng thái của một dự án.
Input: projectId (ID của dự án), status (trạng thái của dự án).
Output: Trả về true nếu cập nhật thành công, false nếu có lỗi.

## 2.Analysis class to design element map
