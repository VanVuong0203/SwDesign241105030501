# Lab 2: Phân tích ca sử dụng hệ thống "Payroll System"

## 1. Phân tích ca sử dụng Login

### Xác định các lớp phân tích
#### Lớp 1: User
 - Mô tả: Đại diện cho người dùng của hệ thống (actor), bao gồm các thuộc tính cơ bản để xác thực.
 - Thuộc tính:
   + username: Tên người dùng đăng nhập
   + password: Mật khẩu đăng nhập
 - Nhiệm vụ: Cung cấp thông tin đăng nhập và khởi động quy trình xác thực thông qua LoginController.
#### Lớp 2: LoginController
 - Mô tả: Điều khiển quá trình đăng nhập, nhận yêu cầu từ User và giao tiếp với AuthenticationService để xác thực.
 - Nhiệm vụ:
   + Nhận thông tin đăng nhập từ User.
   + Gửi thông tin cho AuthenticationService để xác thực.
   + Xử lý kết quả xác thực và điều hướng người dùng nếu đăng nhập thành công hoặc thông báo lỗi khi thất bại.
#### Lớp 3: AuthenticationService
 - Mô tả: Xử lý logic xác thực, kiểm tra thông tin đăng nhập với cơ sở dữ liệu.
 - Thuộc tính:
   + isValid: Boolean, đại diện cho kết quả xác thực.
 - Nhiệm vụ:
   + Kiểm tra username và password với thông tin trong UserDatabase.
   + Trả về kết quả xác thực cho LoginController.
#### Lớp 4: UserDatabase
 - Mô tả: Đại diện cho cơ sở dữ liệu chứa thông tin người dùng, được AuthenticationService sử dụng để xác thực.
 - Thuộc tính:
   + users: Danh sách người dùng với thông tin đăng nhập.
 - Nhiệm vụ:
    + Cung cấp thông tin đăng nhập cần thiết cho AuthenticationService để xác thực người dùng.

### Biểu đồ tuần tự cho ca sử dụng Login
![Sequence Diagram](https://www.planttext.com/api/plantuml/png/V9AnJiCm48PtFyMDhKJ5dW4LbO41iL0Um4sSn6fo3euJw8WwCB30n82GMY4sAe74GZ9qICLxv0bu1Sv5HQMaUB3aEz_tt_tsPpdlfePhayKHuwvH6avJeLb28UdAXAE18nL8x2aqMaNHHcu_Cw50Ed8Z5Pu8dKjN_BfXSGVSy05F1MFs19szJQO3ns5Tp1B8A8yy5f1N4qXucfuhxR6DsnRGAEn0BhJqHpqjF9laKTfQ4NT-S6tMM6ofwyqwqDVP2FAwU48mOVM60HY9WC77Irq-IF2gTmgrV8cUhMkpzMheR6-oh-lYaS3b9GphOcxWBBC1Kpt7C9GKYQ6rD4gYhxPss-JY5l95DNLfXBfyTQ5bT2PsVR96j1dZaO75pM9CW-3t2z2a4mp1jVCoeDLWlctEeJf9GXc4rezx8YnkIHCXa5o1Hxah13UiPXWoGMf_TCXO0uEwcCh_TGu9DSPb_zUhXnXKKmLHNTv99j1ZNThi3sRi2m00__y30000)

- Giải thích:
User bắt đầu quy trình bằng cách gửi thông tin đăng nhập cho LoginController.
LoginController gọi hàm verifyCredentials của AuthenticationService để xác thực thông tin.
AuthenticationService truy vấn UserDatabase để tìm thông tin người dùng.
UserDatabase trả về kết quả tìm kiếm cho AuthenticationService.
AuthenticationService gửi kết quả xác thực (true/false) về cho LoginController.
Dựa trên kết quả, LoginController sẽ điều hướng User đến giao diện chính nếu đăng nhập thành công, hoặc hiển thị thông báo lỗi nếu đăng nhập thất bại.

### Biểu đồ lớp phân tích Login
![Class Diagram](https://www.planttext.com/api/plantuml/png/d5BBJWCn3BpxAwoUYjGSk4O8zS6HMyK7cAnR8gLE5NkB4EBBEF19_0ARLTNIxPwQYvNnUCOPvVVxPwv6nTfTWf185L-K2tu2TiTXsrs4TknnRINAzWZlE-9xBiq5Z4YjlR5O36Gy7NBkF2vpJam2Nt3qUixRAAiiLd9A9rl4LF7fq7nsvJkckJWl4REikHnYu9FoWKlSVAmADvL3IMzqgIazaT4hwLby4wMfZIlDJg7YTRoFTt8_mGVd-ZhCmDVG5OPmfJhtsDVn9teCb9B2UFV__CNo7gCO5mgc07EMfdu5W3y0003__mC0)

- Giải thích các lớp trong biểu đồ:
User:

Thuộc tính: username, password để lưu thông tin đăng nhập của người dùng.
Phương thức: authenticate(password: String): Boolean để kiểm tra tính hợp lệ của mật khẩu được cung cấp.
LoginController:

Phương thức: login(username: String, password: String): Boolean, là điểm vào cho ca sử dụng Login. Phương thức này thực hiện xử lý yêu cầu đăng nhập và gọi AuthenticationService để xác minh thông tin đăng nhập.
AuthenticationService:

Phương thức: verifyCredentials(username: String, password: String): Boolean, xác minh thông tin đăng nhập của người dùng bằng cách tương tác với lớp UserDatabase.
UserDatabase:

Phương thức: findUser(username: String): User tìm kiếm và trả về đối tượng User dựa trên username. Đây là nơi lưu trữ và quản lý dữ liệu người dùng.
