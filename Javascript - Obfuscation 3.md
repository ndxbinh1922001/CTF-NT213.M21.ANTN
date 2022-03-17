# Javascript - Obfuscation 3
## Solution
Khi truy cập vào website thì chỉ có 1 cái form và không thấy thành phần của website.

![image](https://user-images.githubusercontent.com/86184794/158736371-63ec5d29-48f8-4b84-b9a4-784b17090075.png)

Để thấy được thành phần của website thì em sẽ nhập 1 password bất kỳ vào.

![image](https://user-images.githubusercontent.com/86184794/158736468-21a4e826-3216-4ff1-83c6-bd1761c09fe9.png)

Ta thấy trong file có đoạn code javascript chứa hàm dechiffre() dùng để decode chuỗi nhập vào ra được kết quả thì cho qua hàm String.fromCharCode() để lấy được password.

![image](https://user-images.githubusercontent.com/86184794/158737320-913f71ff-4fc0-4319-b3ad-30dfc480ac1f.png)

Đây là kết quả sau khi decode chuỗi của chương trình.

Sau đó đưa chuỗi kết quả này vào hàm String.fromCharCode() để tạo ra password.

![image](https://user-images.githubusercontent.com/86184794/158737594-fa8b14dc-2a31-4bd1-b109-5d86803b3692.png)

Flag: 786OsErtk12





