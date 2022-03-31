# CSRF - token bypass
## Solution


Ban đầu challange cho chúng ta 1 form để đăng nhập như thế này.

![image](https://user-images.githubusercontent.com/86184794/161018385-0a8797ca-98b8-4043-bb4e-09c9930ed6fc.png)


Việc đầu tiên của em là vào đăng ký tài khoản.

![image](https://user-images.githubusercontent.com/86184794/161018525-0c042931-4c64-4cb8-baf3-b4dc6b273b0d.png)

Tài khoản: binh

Mật khẩu: 1

![image](https://user-images.githubusercontent.com/86184794/161018648-00e16e86-931e-491b-b42b-039beb82cbbb.png)


Khi đăng nhập vào thì xuất hiện một đường link điều hướng đến profile của em.

![image](https://user-images.githubusercontent.com/86184794/161018880-3f9659fd-5b1e-4fc9-bf4e-e7584f50b716.png)


Trong profile thì có 3 tab là Contact,Profile và Private. Hiện tại em đang ở tab profile nên có một form update profile.

![image](https://user-images.githubusercontent.com/86184794/161019147-aff9f00f-f831-408e-b2cb-0d460152e4c8.png)

Như khi em thử submit thì không được vì em không phải là admin.

![image](https://user-images.githubusercontent.com/86184794/161019348-4e5e56e3-7e2b-4937-b579-38a53121631c.png)

Khi vào tab Private thì xuất hiện tài khoản của em chưa được kích hoạt bới quản trị viên.


![image](https://user-images.githubusercontent.com/86184794/161019677-e2d1d10d-91ed-42fb-83ea-370d18e4504f.png)

Bên tab Contact thì em có thể submit một form được. Và form này em có thể khai thác được.

![image](https://user-images.githubusercontent.com/86184794/161020172-120cf87a-e2f8-47c0-a6fd-2ba3bc2066a3.png)

Quay trở lại form đăng nhập em thấy nút Status đã bị disable theo kinh nghiêm và cảm nhận của em khi chơi rất nhiều bài root me thì Status có thể là quyền admin. Nên em thử tìm cách kích hoạt nút Status lên thử.

![image](https://user-images.githubusercontent.com/86184794/161026573-6fc834fb-8238-4564-b42d-b250171b157c.png)


Trong devtool thì em thấy có một form submit như thế này. Em thử xóa thuộc tính diasble đi rồi sau đó checked vào xong submit thì vẫn không được.

Do đó em nghĩ ra một ý tưởng là form submit này nó đưa đến server nên em copy cái form submit này em qua bên tab contact để nó chạy thử có gửi được đến server hay không.

Và một điều nữa chúng ta cần chú ý là ở cuối form có một input token

![image](https://user-images.githubusercontent.com/86184794/161026791-dcbeb7be-f002-49ae-81f2-eea7400c116c.png)

Để submit được form này thì chúng ta phải có được token này nhưng mỗi lần load trang thì token lại thay đổi vì thế muốn lấy token thì khi server trả response về cho client thì không để cho web reload mà chúng ta phải lấy token đó gửi lại cho server.

```
<form action="http://challenge01.root-me.org/web-client/ch23/?action=profile" method="post" id="form" enctype="multipart/form-data">
                <input id="username" type="text" name="username" value="1337">
                <input id="status" type="checkbox" name="status" checked >
                <input id="token" type="hidden" name="token" value="" />
                <button type="submit">Submit</button>
</form>

<script>

                var xhttp = new XMLHttpRequest();
                xhttp.open("GET", "http://challenge01.root-me.org/web-client/ch23/?action=profile", false);
                xhttp.send();

                // extraction du token
                var token_admin = (xhttp.responseText.match(/[abcdefghijklmnopqwxyz0123456789]{32}/));

                // insertion du token dans notre formulaire
                 document.getElementById('token').setAttribute('value', token_admin)

                // envoi du formulaire
                document.getElementById('form').submit();
</script>
```




Trong form ở trên thì đường dẫn em sẽ submit đến tab profile với phương thức là post và nút Status  em đã chuyển thành checked có nghĩa là đã được kích hoạt.


![image](https://user-images.githubusercontent.com/86184794/161029022-61e83f66-c03a-4b1c-ae5b-b344731b5588.png)

Chờ một lúc thì em được kết quả như sau.

![image](https://user-images.githubusercontent.com/86184794/161035456-24228251-9fe3-45ad-92b2-c636fe1aa9af.png)

Flag: Byp4ss_CSRF_T0k3n-w1th-XSS
