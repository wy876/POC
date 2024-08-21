## 锐捷RG-UAC统一上网行为管理与审计系统管理员密码泄露

## 影响版本
```
锐捷RG-UAC统一上网行为管理审计系统
```

## fofa
```
title="RG-UAC登录页面" && body="admin"
```

## 漏洞复现
右键查看源代码 搜索 admin 即可找到admin md5密码
![](./assets/20231121190212.png)
