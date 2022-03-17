# HTML - disabled buttons
## Solution 
![image](https://user-images.githubusercontent.com/86184794/158715043-95e778a5-d758-48a3-b690-3c8ef4f339d0.png)

Đây là giao diện web của đề bài. Giao diện này có 1 trường input và 1 button nhưng đều bị disabled.
Vào devtool thì ta thấy input và button có thuộc tính disabled. Thuộc tính disabled xác định rằng trường dữ liệu đầu vào bị vô hiệu hóa, tức là không thể sử dụng, không thể click vào và giá trị cũng không được gửi khi biểu mẫu gửi đi.

![image](https://user-images.githubusercontent.com/86184794/158715364-19a53c17-43b2-45ae-b502-839993e8ccdf.png)

Để có thể submit form này thì chúng ta cần loại bỏ thuộc tính disabled trong 2 thẻ input với button này.
![image](https://user-images.githubusercontent.com/86184794/158716298-1b6f4bb3-49f1-49a3-837b-b0dbc089b2ba.png)

Sau khi loại bỏ thuộc tính disabled thì chúng ta có thể nhập bất cứ từ gì vào để lấy được flag.

![image](https://user-images.githubusercontent.com/86184794/158719381-4405fa74-812b-4d98-b25a-c48fcfd95a73.png)

Flag: HTMLCantStopYou
