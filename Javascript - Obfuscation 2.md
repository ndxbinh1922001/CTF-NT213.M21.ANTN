# Javascript - Obfuscation 2
## Solution
Khi truy cập vào trang web ta thấy website không có gì cả.

![image](https://user-images.githubusercontent.com/86184794/158730272-bd2cfcd3-5bf1-4efb-abdd-0d4218a09ba2.png)

Nhưng ta thấy một biến pass lưu giá trị 1 chuỗi như sau:

![image](https://user-images.githubusercontent.com/86184794/158730447-5ad0cb3c-ee39-46f5-b7f9-a3c569ae7bff.png)

Đưa giá trị vào console ta được.

![image](https://user-images.githubusercontent.com/86184794/158730496-f6c85c36-ab3d-488c-abf5-8ee4af71d38c.png)

Ta thấy trong hàm unescape() có chứa một hàm nữa. Mà hàm này ở định dạng url nên ta sẽ decode url chuỗi trong hàm unescape()

![image](https://user-images.githubusercontent.com/86184794/158730686-1052ec88-a4ba-41f7-a48d-aae4fa0190fd.png)

Sau đó ta chạy hàm này trong console
![image](https://user-images.githubusercontent.com/86184794/158730771-88ab5926-b74a-4d14-8c4d-91efd42d3ef3.png)

Flag: hDufjdki156

