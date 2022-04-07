# SQL injection - String
## Solution

![image](https://user-images.githubusercontent.com/86184794/162109970-7a9fd1e0-8d33-4cd7-b319-abad0c3b1138.png)

Ban đầu challenge cho em một giao diện gồm 1 số liên kết và các tab Home, Search, Login.

Sau khi vào các liên kết thì challenge chỉ xuất ra các đoạn văn bản nên không thể khai thác ở những liên kết này được.

Còn tab Home là tab hiện tại khi vừa vào challenge đã xuất hiện.

![image](https://user-images.githubusercontent.com/86184794/162110195-cf5d5ab8-1db8-4709-9ea9-04401895838d.png)

Tab Search cho em 1 ô input có thể khai thác được.

![image](https://user-images.githubusercontent.com/86184794/162110256-155b4ca0-3bc5-4f07-adb0-2f2c39e77ff6.png)

Tab Login có 1 form đăng nhập.

Như vậy giờ em thử 2 tab Search và Login xem thử có thể khai thác được không.

Em thử nhập input `1' --` vào các ô input xem sao.

![image](https://user-images.githubusercontent.com/86184794/162110450-d0de2c7b-5b2b-4693-afc7-97202c6386c0.png)

Ở input trong tab Search thì em thấy input không được làm sạch. Khả năng cao input này có thể khai thác được.

Giờ em thử nhập nhập vào input `admin' --` để lấy được mật khẩu của tài khoản admin.

![image](https://user-images.githubusercontent.com/86184794/162110703-420c5951-c2c7-4daf-b4c0-4329d849d89c.png)

Nhưng không thể tìm được user nào tên là admin. Có thể trong tab Search này câu query không search trong bảng lưu username với password.

![image](https://user-images.githubusercontent.com/86184794/162110993-3f799277-3c4a-40cd-8984-e46d15aaec6f.png)

Sau khi search google thì em tìm ra cách để xem được các bảng trong database

Như vậy giờ em chỉ cần select ra tên bảng(name) và câu lệnh tạo ra bảng(sql) thì có thể sẽ lấy được thông tin của các trường trong bảng lưu username, password. Nếu biết được tên bảng và các trường đó thì em dùng câu truy vấn select username với password của bảng chứa 2 trường này thì sẽ được thông tin của tài khoản admin.

Ở đây thì em dùng hàm UNION để kết hợp 2 câu truy vấn lại với nhau.

`admin' union select name, sql from sqlite_master -- `

![image](https://user-images.githubusercontent.com/86184794/162111803-0cdda1f0-957a-442e-ae0d-eb28ce124215.png)

Như vậy em đã có được thông tin của bảng users có 2 trường là username, password giờ em sẽ select nó ra để lấy thông tin tài khoản của user admin.

![image](https://user-images.githubusercontent.com/86184794/162112010-085d8daf-5a34-4723-bc60-75fdcaacaaab.png)

Flag: c4K04dtIaJsuWdi
