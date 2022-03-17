# Javascript - Source
## Solution
Khi truy cập vào trang web chương trình hiện ra một thông báo để nhập mật khẩu nhưng khi sử dụng devtool để xem thành phần của chương trình thì không có gì. Bởi vì chương trình này sử dụng thuộc tính onload cho thẻ body. Khi thẻ body được load lên thì chương trình sẽ gọi tới hàm login().
Javascript - Source

![image](https://user-images.githubusercontent.com/86184794/158722060-27bebffe-8dcd-4d0d-88ab-7ac2a6c27b1f.png)

Để xem thành phần của website thì chúng ta nhập bất kỳ password nào vào để hàm login() chạy lỗi thì sẽ xem được.

![image](https://user-images.githubusercontent.com/86184794/158722214-ea58bc6b-b5e3-487a-93af-187c28520cd6.png)

Như vậy chúng ta vào file index để xem function login() như thế nào.

![image](https://user-images.githubusercontent.com/86184794/158722364-9e8866c2-0787-4b58-aaf8-27e864be1f52.png)

Ta thấy chương trình sẽ kiểm tra password với chuỗi "123456azerty".

![image](https://user-images.githubusercontent.com/86184794/158722494-336bdcd9-0f31-40b0-b0d0-96044480692b.png)

Ta nhập password là "123456azerty".

![image](https://user-images.githubusercontent.com/86184794/158722556-f3b01267-bfa0-4a76-adc1-f4700a3a9b51.png)

Flag: 123456azerty


