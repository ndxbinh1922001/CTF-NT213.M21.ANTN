# SQL injection - Numeric
## Solution

![image](https://user-images.githubusercontent.com/86184794/162143686-9cbc16a6-1302-4cb5-98a8-9db7fe2886d2.png)

Ban đầu challenge cho em một website với 1 số liên kết và 2 tab là Home và Login. Bài này khá giống với bài SQL injection - String.

![image](https://user-images.githubusercontent.com/86184794/162143996-2c73b374-fc60-41cd-91b7-eee81505dee5.png)

Để khai thác bài này em sử dụng liên kết ở trên hình

![image](https://user-images.githubusercontent.com/86184794/162144091-6cc725f9-c16b-4a51-89a9-94eafd3d68b0.png)

Vì trong liên kết này em thấy chương trình cho phép nhập input vào tham số trên đường dẫn. 

Giờ em sẽ bắt đầu khai thác chương trình bằng cách nhập vào input `admin' union select name, sql from sqlite_master -- `, vì bài này khá giống bài SQL injection - String ở đây em sẽ không giải thích chi tiết tại sao em lại select những trường này trong bảng sqlite_master.

![image](https://user-images.githubusercontent.com/86184794/162144914-54a5ab88-873c-4542-8825-c5377571c93d.png)

Nhưng khi nhập vào thì challenge báo lỗi như trên. 

Em để ý trên đề bài challenge có gợi ý là Numeric và tên tham số trên url cũng là news_id nên rất có thể tham số chỉ nhận số nguyên do đó em sẽ nhập thử input `1 union select name, sql from sqlite_master -- `

![image](https://user-images.githubusercontent.com/86184794/162145963-a6d47229-310d-43da-96ce-25c414d7cc27.png)

Nhưng lại bị lỗi tiếp. Lỗi này là do khi em dùng union thì output của lệnh select phía sau không giống cấu trúc của output lệnh phía trước. Input này `1 union select name, sql from sqlite_master -- ` khi em chạy ở bài SQL injection - String thì lúc đó hên là output ở lệnh select ở trước cũng là 2 cột nên không bị lỗi. Vì vậy giờ em thử thêm cột vào output của lệnh select sau union thử xem sao.

Input:

```
1 union select name, sql, 1 from sqlite_master -- 
```

![image](https://user-images.githubusercontent.com/86184794/162146765-b31cfd82-dde6-415b-92fc-8cc470150968.png)

Như vậy là em đã có được thông tin của các bảng trong database.

Tiếp theo nhập input để lấy thông tin trong bảng users.

```
1 union select username, password, Year from users -- 
```

![image](https://user-images.githubusercontent.com/86184794/162147373-64370e7c-0923-4d84-96c4-f537fea32717.png)

Nhưng output nó ra như thế này. Em không biết là output nó ra là username hay password nữa. Giờ phải thử thôi. Em thấy có 2 cái cột được in ra và 1 cột vì một số lí do nào đó không được in ra hoặc cũng có thể nó không chứa dữ liệu.

Giờ em thử ví dụ cột đầu tiên không được in ra nên em sẽ đưa username, password vào 2 cột phía sau thử.
```
1 union select Year, username, password from users -- 
```
Được kết quả nhau sau

![image](https://user-images.githubusercontent.com/86184794/162148380-3db3c7e9-2be0-492e-8bde-0e5dfd8f5319.png)

Flag: aTlkJYLjcbLmue3
