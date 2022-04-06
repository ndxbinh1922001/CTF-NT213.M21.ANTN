# SQL injection - Authentication - GBK
## Solution
Ban đầu challenge cho một form đăng nhập như thế này.

![image](https://user-images.githubusercontent.com/86184794/162013531-863cf56a-3668-4359-9132-d2267d09ebfa.png)

Trong DOM Element cũng không có gì đặc biệt để khai thác.

![image](https://user-images.githubusercontent.com/86184794/162013797-cb1c5391-3796-48a1-8972-cf053f84539a.png)

Thử nhập username password rồi submit form xem như thế nào.

Username: 1

Password: 1

![image](https://user-images.githubusercontent.com/86184794/162015026-b1075fa2-6b17-4a8a-9ce0-1a63f4bbe2ba.png)

Giờ em thử nhập `admin' --` cho username và password 1 thử xem sao.


![image](https://user-images.githubusercontent.com/86184794/162015901-57bca620-1d6f-4232-a86b-19e61c8d016f.png)

Nhưng vẫn không khai thác được có thể là server đã làm sạch input.

![image](https://user-images.githubusercontent.com/86184794/162016365-bb56fe30-b3e9-4ea7-a7be-e2c73e3fc807.png)

Theo gợi ý của challenge thì challenge này có liên quan đến tiếng trung quốc.

Và keyword GBK em search được trên google thì cái này là bộ mã hóa kí tự của tiếng trung quốc. Em nghĩ hướng này có thể khai thác được. Đây là trang tài liệu nói về [bộ mã hóa GBK](https://en.wikipedia.org/wiki/GBK_(character_encoding)#cite_note-gb18030-2005-7).

Và em cũng search được cái bộ mã hóa GBK này có liên quan đến thủ thuật "Bypassing the addslash". Như vậy có thể search làm sạch input bằng cách thêm những dấu backslash "\" này vào trước các kí tự đặc biệt như (,),". Ví dụ input của chúng ta là `admin' --` thì server sẽ thêm những dấu backslash "\"này vào thì input sẽ trở thành `admin\' --` như vậy câu query của chúng ta đã sai cú pháp nên không có tác dụng.

Bây giờ nhiệm vụ của em là sử dụng bộ mã hóa GBK này để bypass backslash "\".

Sau khi nghiên cứu bộ mã hóa GBK thì em biết để tạo ra một tiếng trung quốc thì cần có 2 byte nhưng mà em thấy thì byte thứ 2 mình có thể chọn là `%5c`,`%5c` là dấu backslash "\" 

![image](https://user-images.githubusercontent.com/86184794/162020264-82f6b403-1344-401b-9c87-86d85876991e.png)

Như trên hình thì để chọn được byte thứ 2 là `%5c` thì ta chỉ có thể chọn được các vùng được khoanh đỏ trên hình.

Tóm lại ý tưởng để khai thác bài này như sau:
- Khi ta nhập input vào là `admin' -- `
- Server sẽ làm sạch input bằng cách thêm backslash "\" `admin\' --`
- Như vậy thì câu query của em sẽ sai. Thế nên em đổi input lại thành `%81' -- `
- Server sẽ thêm backslash thì bakcslash sẽ kết hợp với `%81` trước đó để tạo thành tiếng trung quốc như này: `玕` (cái này chỉ là từ ví dụ em copy trên mạng thôi)
- Như vậy thì kí tự `'` sẽ không bị loại khỏi câu query. 

Bây giờ ta dùng Burp Suite để chạy thử input `%81%27 or 1=1 -- `

![image](https://user-images.githubusercontent.com/86184794/162024464-203a9b51-9b0a-464a-8b99-8b6f60bcdb81.png)

![image](https://user-images.githubusercontent.com/86184794/162024504-151a70da-b64d-40c3-9a02-8f6ea44b3863.png)
 
 FLag: iMDaFlag1337!
