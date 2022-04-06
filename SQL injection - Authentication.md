# SQL injection - Authentication
## Solution

Challenge này cung cấp cho chúng ta một cái form để khai thác như sau.

![image](https://user-images.githubusercontent.com/86184794/161976062-e7489432-02a5-49aa-a57d-c72566dff0fa.png)

![image](https://user-images.githubusercontent.com/86184794/161976230-14fb4751-9949-4d83-877a-0fe2175cb6d3.png)

Trong DOM Element cũng không có gì đặc biệt.

Giờ em thử nhập thử username với password xem sao.

Username: admin
Password: admin

![image](https://user-images.githubusercontent.com/86184794/161976418-98cc2ebe-4135-4979-8e24-67959fb9c2d4.png)

Lỗi không tìm thấy user/password.

Như vậy ở server khi xử lý sẽ chạy 1 đoạn code SQL để tìm kiếm username/password

Theo em thì nó sẽ sử dụng câu lệnh

```
SELECT  *  FROM table_username_password WHERE username="username_đã_nhập" AND password="password_đã_nhập"
```

Giờ để khai thác lỗi chỗ này thì username em sẽ nhập là "admin' --" có nghĩa là

```
SELECT  *  FROM table_username_password WHERE username="admin' --" AND password="password_đã_nhập"
```

Mà trong ngôn ngữ SQL những kí tự sau sau "--" đều là comment như vậy thì câu truy vấn của chúng ta chỉ là

```
SELECT  *  FROM table_username_password WHERE username="admin' 
```

Như vậy nếu trong database có username là "admin" thì chúng ta đã bypass được quá trình kiểm tra đăng nhập.

![image](https://user-images.githubusercontent.com/86184794/161979070-d4a58a99-9423-4e33-86e4-3f7230023972.png)

Username: admin' --
Password: 123

![image](https://user-images.githubusercontent.com/86184794/161979199-f42184e1-d7a6-4ebc-a02b-3abf2e657ccb.png)

Ta đã có được password của admin: t0_W34k!$

Flag: t0_W34k!$"
