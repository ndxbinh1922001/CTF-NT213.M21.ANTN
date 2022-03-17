# Javascript - Native code
## Solution
Khi truy cập vào website thì một form xuất hiện yêu cầu nhập mật khẩu vào và trong thành phần của website không có gì cả

![image](https://user-images.githubusercontent.com/86184794/158732748-6e3f4961-79c0-41aa-8c7d-346b0ce82607.png)

Do đó em sẽ nhập bất kỳ kí tự nào để hiện ra thành phần của webite.

![image](https://user-images.githubusercontent.com/86184794/158732826-f3d1c89b-c596-479a-812c-2682631f0d54.png)

Website không có thành phần gì nhưng có một chuỗi mã hóa gần các ký tự rất đặc biệt.

Em thử copy đoạn kí tự đặc biệt này mang vào console để chạy thử thì kết quả nó lại hiện form yêu cầu nhập mật khẩu như lúc mới vào website nên em đoán đoạn ký tự này là đoạn code của chương trình nhưng được mã hóa.

![image](https://user-images.githubusercontent.com/86184794/158733058-86c89390-5270-4bec-b613-bac79d4ae83f.png)

Em copy 1 đoạn mã ngắn lên google search  để tìm cách decode nó.

Link tham khảo: https://reverseengineering.stackexchange.com/questions/22679/how-can-i-deobfuscate-this-javascript-code

Theo như link này thì cặp ngoặc trong cuối đoạn test nếu được thay thế bằng chuỗi toString() thì có thể in ra đoạn mã đó. Có nghĩa là thay vì mình chạy đoạn code đó thì mình chuyển đoạn code đó thành chuỗi rồi in ra màn hình.

![image](https://user-images.githubusercontent.com/86184794/158733468-5a5e1a30-03f9-4b7c-81ca-fcd7fd9db551.png)

Đây là kết quả sau khi decode đoạn code này.

Trong đoạn code ta thấy chương trình so sánh password với chuỗi "toto123lol"

Flag: toto123lol

