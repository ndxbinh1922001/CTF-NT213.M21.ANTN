# SQL Truncation
## Solution

![image](https://user-images.githubusercontent.com/86184794/162600940-27dae0dd-67d3-4956-94b3-fe9967aae9d6.png)

Ban đầu challenge cho chúng ta giao diện web như thế này. Trong challenge có 3 tab chúng ta cần chú ý là Home(trang hiện tại), Register, Administration.

![image](https://user-images.githubusercontent.com/86184794/162601012-19e45d1f-270d-4b96-8fd8-831f751e9814.png)

Nhưng mà trong tab Register em thấy chương trình có comment 1 đoạn SQL như vậy giờ em đã biết độ dài của các trường trong table user.

Theo như gợi ý của đề bài thì challenge này có liên quan đến keyword `truncate`. Em search google xem qua 1 số writeup thì biết được truncate ở đây là không phải là hàm truncate() hay là từ khóa truncate mà là lỗi `Truncate Error`.

Lỗi `Truncate Error` này xảy ra khi dữ liệu đưa vào lớn hơn độ dài được khai báo tại trường này trong Database, và để dữ liệu này lưu vào được Database nó sẽ được cắt ra cho vừa độ dài mà được khai báo trong Database.

Như vậy ý tưởng khai thác bài này của em là ở tab `Register`. Đầu tiên khi em nhập input là 1 chuỗi thiệt dài như thế này `admin                               binh` thì khi vào server nó sẽ kiểm tra cái input  `admin                               binh` này khác với user `admin` trong Database nên sẽ được thông chốt. Sau đó vào database thì input sẽ được cắt ra cho vừa đủ độ dài như vậy input lúc này sẽ đổi thành `admin`. Do đó chúng ta đã thêm được tài khoản admin vào Database.

![image](https://user-images.githubusercontent.com/86184794/162601322-c87e1106-065b-4959-91d9-090b06654ae3.png)

Username: `admin                               binh`
Password: `111111111` (Password tối thiểu là 8 kí tự)


![image](https://user-images.githubusercontent.com/86184794/162601349-373b755e-9cbb-47bf-8a5f-2232c5de891a.png)

Flag: J41m3Qu4nD54Tr0nc


