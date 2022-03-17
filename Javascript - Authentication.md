# Javascript - Authentication
## Solution

Chương trình cho chúng ta một form đăng nhập. Như vậy nếu chúng ta tìm được username với password thì sẽ pass được thử thách.

![image](https://user-images.githubusercontent.com/86184794/158720376-4e6819fa-9178-4305-b212-a3f3c67e79f1.png)

Ta thấy khi button đăng nhập được click thì chương trình sẽ gọi đến hàm login(). Như vậy chúng ta vào file javascript của chương trình để xem hàm login() xử lý như thế nào.

![image](https://user-images.githubusercontent.com/86184794/158720570-6e4f2bbb-e74a-4e06-8f55-d4c510eac359.png)

Vào devtool -> Sources -> login.js chúng ta sẽ có được code của file login.js
![image](https://user-images.githubusercontent.com/86184794/158720671-37825cc1-39fb-46ee-ba13-9599a200fcf5.png)

Ta thấy username được kiểm tra với chuỗi "4dm1n" và password được kiểm tra với chuỗi "sh.org". Vậy khi chúng ta nhập username với password là "4dm1n", "sh.org" sẽ pass được form đăng nhập này.
![image](https://user-images.githubusercontent.com/86184794/158721006-8e3f5803-d753-443a-9bd0-b6a9d9ae55a2.png)
Flag: sh.org
