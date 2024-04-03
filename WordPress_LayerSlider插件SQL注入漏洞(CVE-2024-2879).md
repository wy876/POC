## WordPress_LayerSlider插件SQL注入漏洞(CVE-2024-2879)

## fofa
```
"wp-content/plugins/LayerSlider/"
```


## nuclei
```
id: CVE-2024-2879

info:
  name: >
    LayerSlider 7.9.11 - 7.10.0 - Unauthenticated SQL Injection
  author: topscoder
  severity: critical
  description: >
    The LayerSlider plugin for WordPress is vulnerable to SQL Injection via the ls_get_popup_markup action in versions 7.9.11 and 7.10.0 due to insufficient escaping on the user supplied parameter and lack of sufficient preparation on the existing SQL query.  This makes it possible for unauthenticated attackers to append additional SQL queries into already existing queries that can be used to extract sensitive information from the database.
  reference:
    - https://www.wordfence.com/threat-intel/vulnerabilities/id/3fddf96e-029c-4753-ba82-043ca64b78d3?source=api-prod
  classification:
    cvss-metrics: CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:H
    cvss-score: 9.8
    cve-id: CVE-2024-2879
  metadata:
    fofa-query: "wp-content/plugins/LayerSlider/"
    google-query: inurl:"/wp-content/plugins/LayerSlider/"
    shodan-query: 'vuln:CVE-2024-2879'
  tags: cve,wordpress,wp-plugin,LayerSlider,critical

http:
  - method: GET
    redirects: true
    max-redirects: 3
    path:
      - "{{BaseURL}}/wp-content/plugins/LayerSlider/readme.txt"

    extractors:
      - type: regex
        name: version
        part: body
        group: 1
        internal: true
        regex:
          - "(?mi)Stable tag: ([0-9.]+)"

      - type: regex
        name: version
        part: body
        group: 1
        regex:
          - "(?mi)Stable tag: ([0-9.]+)"

    matchers-condition: and
    matchers:
      - type: status
        status:
          - 200

      - type: word
        words:
          - "LayerSlider"
        part: body

      - type: dsl
        dsl:
          - compare_versions(version, '>= 7.9.11', '<= 7.10.0')
```
