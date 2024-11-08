# Vben-Admin存在硬编码漏洞
<font style="color:rgba(0, 0, 0, 0.84);">Vue Vben Admin是一个免费开源的中端和后端模板。采用最新的vue3、vite、TypeScript等主流技术开发，开箱即用的中后端前端解决方案也可供学习参考。Vue Vben存在硬编码漏洞</font>

## fofa
```javascript
icon_hash="-317536629"
```

![](https://cdn.nlark.com/yuque/0/2024/png/29512878/1729264064913-c5ad6880-499b-442e-9fee-00d4eb8fa551.png)

## poc
登录页面，右击查看源代码，搜索index，进入该js页面

![](https://cdn.nlark.com/yuque/0/2024/png/29512878/1730100317021-035ebb28-c6be-490c-aaf7-20bdc01dab17.png)

该页面硬编码登录账号密码

![](https://cdn.nlark.com/yuque/0/2024/png/29512878/1730100355251-30a27295-5a99-4dc4-8114-4859ca2fb8eb.png)

使用账号密码登录系统

![](https://cdn.nlark.com/yuque/0/2024/png/29512878/1730128898635-bddc9b02-c118-4394-87d6-316664320abb.png)



