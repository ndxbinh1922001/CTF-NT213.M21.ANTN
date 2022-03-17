# Javascript - Obfuscation 1
## Solution
Khi vào website thì chương trình yêu cầu nhập password nhưng khi kiểm tra thành phần thì không có gì cả.

![image](https://user-images.githubusercontent.com/86184794/158726304-589d73ee-f7c2-4763-863c-145925fa1247.png)

Để xem được thành phần thì em nhập bất kỳ kí tự nào.
![image](https://user-images.githubusercontent.com/86184794/158726401-eeffc6fb-3705-4991-8178-f6d614e43d3c.png)
Đây là thành phần của website nhưng cũng không có gì. Nhưng khi vào Sources kiểm tra file html thì có đoạn code javascript trong file html.

![image](https://user-images.githubusercontent.com/86184794/158727369-b95b563c-4f90-4b74-a556-c57f9f54b279.png)

Vì code javacript này là loại text/javascript nên không được hiện lên thành website.
Ta thấy trong chương trình có chuỗi "%63%70%61%73%62%69%65%6e%64%75%72%70%61%73%73%77%6f%72%64" sau đó chương trình mang chuỗi này vào hàm unescape() để decode ra password rồi so sánh với input của chúng ta nhập vào.
Vậy để tìm ra password thì em vào console chạy hàm unescape() với input là chuỗi "%63%70%61%73%62%69%65%6e%64%75%72%70%61%73%73%77%6f%72%64" ta được password là "cpasbiendurpassword"

![image](https://user-images.githubusercontent.com/86184794/158728022-4f5c0fb6-cf1b-43df-a950-ae0ec5112aff.png)
Flag: cpasbiendurpassword
